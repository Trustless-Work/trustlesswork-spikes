---
description: >-
  HTTP 422 returned when an address that receives escrow funds has no trustline
  for the escrow's token.
icon: triangle-exclamation
---

# ESCROW\_RECEIVER\_TRUSTLINE\_MISSING

| Field | Value |
| --- | --- |
| HTTP status | `422 Unprocessable Entity` |
| Error code | `ESCROW_RECEIVER_TRUSTLINE_MISSING` |
| Returned by | Deploy escrow, Update escrow (single-release and multi-release) |

## What it means

Every address that can **receive escrow funds** must hold a [trustline](../../stellar-and-soroban-the-backbone-of-trustless-work/trustlines.md) for the escrow's token. That includes:

* Receivers and the platform address
* Approvers, when funds can be returned to them
* Dispute payout addresses
* The **Trustless Work protocol-fee wallet**

On Stellar, a payment to an account without the trustline fails. If the escrow were deployed anyway, the later **release** would fail on-chain with `Error(Contract, #13)` ("trustline entry is missing for account") and the funds would stay locked in the escrow. The API checks this up front and returns no transaction to sign.

## Example response

The body is [RFC 9457](https://www.rfc-editor.org/rfc/rfc9457) Problem Details. The explanation is `detail`. Structured context is `extensions` (`trustline` and `missing`), not a top-level `message` or `details` field.

{% code overflow="wrap" %}
```json
{
  "type": "https://docs.trustlesswork.com/trustless-work/v2-en/api-rest/errors/escrow-receiver-trustline-missing",
  "title": "Validation Error",
  "status": 422,
  "code": "ESCROW_RECEIVER_TRUSTLINE_MISSING",
  "detail": "Every role that can receive escrow funds must hold a trustline for the escrow token — trustlessWork (protocol fee) (GA6KH5VWPCHBOEF63X57SPX6T4H366YFFKKGCVDBTXT2N7JVL6PJCK7G): no trustline for the escrow token.",
  "instance": "/escrow/single-release/v2/deploy",
  "traceId": "<request correlation id>",
  "extensions": {
    "trustline": "<escrow token contract id>",
    "missing": [
      {
        "address": "GA6KH5VWPCHBOEF63X57SPX6T4H366YFFKKGCVDBTXT2N7JVL6PJCK7G",
        "roles": ["trustlessWork (protocol fee)"],
        "reason": "trustline-missing"
      }
    ]
  }
}
```
{% endcode %}

`extensions.missing[].reason` is one of:

* `trustline-missing`: the account exists but doesn't hold the token. `detail` still says "no trustline for the escrow token".
* `account-missing`: the account doesn't exist on this network. Fund it with XLM first. `detail` says "account does not exist on this network — fund it with XLM first".

## How to fix it

{% tabs %}
{% tab title="Missing role is yours" %}
The listed address belongs to your escrow (receiver, platform, approver, and so on).

{% stepper %}
{% step %}
**Add the trustline from that wallet**

In Freighter, go to **Manage assets → Add asset** and enter the token's code and issuer. You can also send a `changeTrust` operation. Each trustline reserves 0.5 XLM.
{% endstep %}

{% step %}
**Retry the request**

Call deploy or update again with the same payload.
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="Missing role is trustlessWork (protocol fee)" %}
The escrow token isn't supported by the Trustless Work fee wallet on this network yet.

* **Testnet:** use one of the standard tokens: USDC, EURC or PYUSD. See [Supported Tokens](../../stellar-and-soroban-the-backbone-of-trustless-work/supported-tokens.md). If you need a different test token, get in touch with the Trustless Work team.
* **Mainnet:** use a token marked **Live** on [Supported Tokens](../../stellar-and-soroban-the-backbone-of-trustless-work/supported-tokens.md).
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Protocol-fee wallets:

* Testnet: `GA6KH5VWPCHBOEF63X57SPX6T4H366YFFKKGCVDBTXT2N7JVL6PJCK7G`
* Mainnet: `GBWWSOATPLIC72ZBOIM7WJCT7VCAHNWW4QUBZ2H4FORMCCIUM5ZVKSZN`
{% endhint %}

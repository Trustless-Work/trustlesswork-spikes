---
description: >-
  Stablecoins you can use as the escrow asset on Stellar testnet and mainnet,
  with issuer addresses, contract IDs, and faucets.
icon: square-dollar
---

# Supported Tokens

Trustless Work escrows hold a Stellar asset through its **Stellar Asset Contract (SAC)**. When an escrow releases, part of the amount goes to the Trustless Work protocol-fee wallet, so that wallet needs a [trustline](trustlines.md) for the escrow's asset. The tokens below are the ones the fee wallet supports.

{% hint style="warning" %}
**Always pin the issuer, not just the code.** Anyone can issue an asset called `USDC` or `EURC`. An asset is identified by its code **and** issuer address together.
{% endhint %}

## Testnet

{% hint style="info" %}
**Test with the standard tokens below.** They are free from the issuers' faucets. If your project needs a different test token, get in touch with the Trustless Work team and we'll look at adding it.
{% endhint %}

{% tabs %}
{% tab title="USDC" %}
**Issuer:** Circle

**Asset:** [`USDC:GBBD47IF6LWK7P7MDEVSCWR7DPUWV3NY3DTQEVFL4NAT4AQH3ZLLFLA5`](https://stellar.expert/explorer/testnet/asset/USDC-GBBD47IF6LWK7P7MDEVSCWR7DPUWV3NY3DTQEVFL4NAT4AQH3ZLLFLA5)

**Contract (SAC):** `CBIELTK6YBZJU5UP2WWQEUCYKLPU6AUNZ2BQ4WWFEIE3USCIHMXQDAMA`

**Faucet:** [faucet.circle.com](https://faucet.circle.com/). Select **Stellar Testnet** and **USDC**.
{% endtab %}

{% tab title="EURC" %}
**Issuer:** Circle

**Asset:** [`EURC:GB3Q6QDZYTHWT7E5PVS3W7FUT5GVAFC5KSZFFLPU25GO7VTC3NM2ZTVO`](https://stellar.expert/explorer/testnet/asset/EURC-GB3Q6QDZYTHWT7E5PVS3W7FUT5GVAFC5KSZFFLPU25GO7VTC3NM2ZTVO)

**Contract (SAC):** `CCUUDM434BMZMYWYDITHFXHDMIVTGGD6T2I5UKNX5BSLXLW7HVR4MCGZ`

**Faucet:** [faucet.circle.com](https://faucet.circle.com/). Select **Stellar Testnet** and **EURC**.
{% endtab %}

{% tab title="PYUSD" %}
**Issuer:** Paxos (PayPal USD)

**Asset:** [`PYUSD:GBT2KJDKUZYZTQPCSR57VZT5NJHI4H7FOB5LT5FPRWSR7I5B4FS3UU7G`](https://stellar.expert/explorer/testnet/asset/PYUSD-GBT2KJDKUZYZTQPCSR57VZT5NJHI4H7FOB5LT5FPRWSR7I5B4FS3UU7G)

**Contract (SAC):** `CACZL3MGXXP3O6ROMB4Q36ROFULRWD6QARPE3AKWPSWMYZVF2474CBXP`

**Faucet:** [faucet.paxos.com](https://faucet.paxos.com/). Select **PYUSD** on **Stellar Testnet**.
{% endtab %}
{% endtabs %}

**Testnet protocol-fee wallet:** `GA6KH5VWPCHBOEF63X57SPX6T4H366YFFKKGCVDBTXT2N7JVL6PJCK7G`

## Mainnet

| Token | Asset (code : issuer) | Contract (SAC) | Status |
| --- | --- | --- | --- |
| **USDC** (Circle) | [`USDC:GA5ZSEJYB37JRC5AVCIA5MOP4RHTM335X2KGX3IHOJAPP5RE34K4KZVN`](https://stellar.expert/explorer/public/asset/USDC-GA5ZSEJYB37JRC5AVCIA5MOP4RHTM335X2KGX3IHOJAPP5RE34K4KZVN) | `CCW67TSZV3SSS2HXMBQ5JFGCKJNXKZM7UQUWUZPUTHXSTZLEO7SJMI75` | ✅ Live |
| **EURC** (Circle) | [`EURC:GDHU6WRG4IEQXM5NZ4BMPKOXHW76MZM4Y2IEMFDVXBSDP6SJY4ITNPP2`](https://stellar.expert/explorer/public/asset/EURC-GDHU6WRG4IEQXM5NZ4BMPKOXHW76MZM4Y2IEMFDVXBSDP6SJY4ITNPP2) | `CDTKPWPLOURQA2SGTKTUQOWRCBZEORB4BWBOMJ3D3ZTQQSGE5F6JBQLV` | ✅ Live |
| **PYUSD** (Paxos / PayPal USD) | [`PYUSD:GDQE7IXJ4HUHV6RQHIUPRJSEZE4DRS5WY577O2FY6YQ5LVWZ7JZTU2V5`](https://stellar.expert/explorer/public/asset/PYUSD-GDQE7IXJ4HUHV6RQHIUPRJSEZE4DRS5WY577O2FY6YQ5LVWZ7JZTU2V5) | `CCCRWH6Q3FNP3I2I57BDLM5AFAT7O6OF6GKQOC6SSJNDAVRZ57SPHGU2` | ⏳ Pending, not yet supported |
| **USDT0** (Tether, via LayerZero) | [`USDT0:GATISXX6BZ6NC7IKQBY37CJD4SOZL3CYZJWXEDG6JVIY4WBS6KXJHN6Q`](https://stellar.expert/explorer/public/asset/USDT0-GATISXX6BZ6NC7IKQBY37CJD4SOZL3CYZJWXEDG6JVIY4WBS6KXJHN6Q) | `CBSJZEIO5C7KC2SF3MKSNXXJSW5G3VTNBX4ATMKUI3B2MR4JKM4R26YF` | ⏳ Pending, not yet supported |

{% hint style="danger" %}
**Do not create mainnet escrows in a token marked Pending.** Release, dispute resolution and withdrawal pay the protocol fee to the Trustless Work fee wallet. Until that wallet has the trustline, those calls fail on-chain (`Error(Contract, #13)`), and the funds stay in the escrow until the trustline is added.
{% endhint %}

{% hint style="info" %}
PYUSD and USDT0 issuers can **freeze and claw back** balances (`auth_revocable`, `auth_clawback_enabled`). That includes balances held by escrow contracts. USDC and EURC set `auth_revocable` only.
{% endhint %}

**Mainnet protocol-fee wallet:** `GBWWSOATPLIC72ZBOIM7WJCT7VCAHNWW4QUBZ2H4FORMCCIUM5ZVKSZN`

{% hint style="info" %}
**References**

* Circle: [USDC contract addresses](https://developers.circle.com/stablecoins/usdc-contract-addresses) · [EURC contract addresses](https://developers.circle.com/stablecoins/eurc-contract-addresses)
* Paxos: [PYUSD on test networks](https://docs.paxos.com/guides/stablecoin/pyusd/testnet) · PayPal: [PYUSD on Stellar](https://developer.paypal.com/community/blog/pyusd-on-stellar/)
* Stellar: [USDT0 on Stellar](https://developers.stellar.org/docs/tokens/usdt0-layerzero)
{% endhint %}

{% content-ref url="trustlines.md" %}
[trustlines.md](trustlines.md)
{% endcontent-ref %}

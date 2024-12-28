# Tonkeeper Wallet API (DRAFT)

⚠️ This documentation is work-in-progress. Some features are not yet implemented.

* [Definitions](#definitions)UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
* [Payment URLs](#payment-urls)UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
* [Authentication](#authentication-methods)UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
* [Transaction Request](#transaction-request)UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
* [Basic transfers](#basic-transfers)
  * [Payment](#unauthenticated-transfers)UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
  * [Donation](#unauthenticated-donations)UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
  * [Deploy](#unauthenticated-transfers)UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
  * [SignRawPayload](#unauthenticated-transfers)UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
* [Subscriptions](#subscriptions)
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

## Definitions
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
#### Authentication
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
Protocol for identifying the origin of the request (e.g. recipient of funds)UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
with some root of trust. The trust could be linked to the Certificate Authority certificates (Web PKI) embedded in the OS, to a custom record on Tonkeeper backend, or provided implicitly for the embedded services.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

#### Authenticated object
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
The object’s origin has a verified chain of trust.
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
#### Unauthenticated object
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
The object’s origin is unknown and must be verified by the user through some other means unavailable to the wallet application.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

#### Unsigned object
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
The object does not have an explicit cryptographic signature that helps authenticating it directly.
But it may still be authenticated via other means (e.g. over TLS connection).UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

#### Signed object
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
The object is explicitly signed and can be authenticated through the public key.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
That public key is then used to authenticate the object (e.g. pulling it from the list of known origins).

UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
## Payment URLs
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
#### Unauthenticated transfers

```UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
ton://transfer/<address>UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
ton://transfer/<address>?amount=<nanocoins>UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
ton://transfer/<address>?text=<url-encoded-utf8-text>UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
ton://transfer/<address>?bin=<url-encoded-base64-boc>UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
ton://transfer/<address>?bin=<url-encoded-base64-boc>&init=<url-encoded-base64-boc>
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
https://app.tonkeeper.com/transfer/<address>UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
https://app.tonkeeper.com/transfer/<address>?amount=<nanocoins>UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
https://app.tonkeeper.com/transfer/<address>?text=<url-encoded-utf8-text>UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
https://app.tonkeeper.com/transfer/<address>?bin=<url-encoded-base64-boc>UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
https://app.tonkeeper.com/transfer/<address>?bin=<url-encoded-base64-boc>&init=<url-encoded-base64-boc>
```
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
Opens the pre-filled Send screen and offers user to enter the missing data.
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
```
ton://transfer/<address>?UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    amount=<nanocoins>&UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    text=<url-encoded-utf8-text>
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
https://app.tonkeeper.com/transfer/<address>?UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    amount=<nanocoins>&UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    text=<url-encoded-utf8-text>
```
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
Opens a compact confirmation dialog with all data filled-in. UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
User cannot edit any of the info and can only confirm or dismiss the request.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

#### Unauthenticated donations
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
WIP.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

```
https://app.tonkeeper.com/donate/<address>?UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    amounts[]=<nanocoins1>&UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    amounts[]=<nanocoins2>&UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    allow_custom=<0|1>&UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    text=...UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
```
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
Displays a specialized donation/tip interface.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

* `amounts` — array of possible UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHamounts to choose from (max 3)UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
* `allow_custom` (0, 1) — whether UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHwallet allows user-editable amount field or not. Default is `0`.
* `text` — pre-filled comment (optional).UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
#### Unauthenticated contract deploys
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
⚠️ DEPRECATED: use bin/init params (see above)UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

```
https://app.tonkeeper.com/deploy/<address>?UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    amount=<nanocoins>&UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    stateinit=<hex>&UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    [text=<url-encoded-utf8-text>]
```UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

`stateinit` is a required field with hex-encoded bag-of-cells with one StateInit cell.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

Opens a compact confirmation dialog with all data filled-in.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
User cannot edit any of the info and can only confirm or dismiss the request.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

Destination address must be verified as follows (TonWeb example):UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

```jsUQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
const stateInitCell = UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHCell.oneFromBoc(uriparams.stateinit);UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
const hash = await UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHstateInitCell.hash();UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
const address = new UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHAddress(uriparams.address);UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
const valid = (address.hashPart == hash);UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
```
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

#### Unauthenticated NFT transfer
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
```
https://app.tonkeeper.com/transfer/<destination-address>?UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    [nft=<nft-address>&]UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    [fee-amount=<nanocoins>&]UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    [forward-amount=<nanocoins>]
    UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
ton://transfer/<destination-address>?
    [nft=<nft-address>&]UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    [fee-amount=<nanocoins>&]UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    [forward-amount=<nanocoins>] 
```UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

Opens the pre-filled NFT-send screen and offers user to enter the missing data.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
* `to`: (string) destination account ID. Optional.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
* `fee-amount` (decimal string): UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHnanocoins to be sent to the item’s contract for paying fee. All not used TONs should be returned back by NFT. If not specified default UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHvalue will be used - 1 TON.
* `forward-amount` (decimal string): nanocoins to be sent as a UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHnotification to the new owner. If not specified default value will be used - 1 nanoTON.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH


#### Unauthenticated Jetton transfer

```UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
https://app.tonkeeper.com/transfer/<destination-address>?UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    [jetton=<jetton-master-address>&UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH]
    [amount=<elementary units>&]UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    [fee-amount=<nanocoins>&]UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    [forward-amount=<nanocoins>]UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    
ton://transfer/<destination-address>UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH?
    [jetton=<jetton-master-address>&]UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    [amount=<elementary units>&]UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    [fee-amount=<nanocoins>&]UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    [forward-amount=<nanocoins>] UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
```
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
Opens the pre-filled Jetton-send UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHscreen and offers user to enter the missing data.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
* `to`: (string) destination account ID. Optional.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
* `amount` (decimal string): amount of transferred jettons in elementary units.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
* `fee-amount` (decimal string): UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHnanocoins to be sent to the Jetton contract for paying fee. All not used TONs should be returned back by Jetton contract. If not specified default value will be used - 1 TON.
* `forward-amount` (decimal string): nanocoins to be sent as a UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHnotification to the destination account. If not specified default value will be used - 1 UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHnanoTON.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH


UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
#### Transaction Request URL
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
Transaction request can be UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHcommunicated to the wallet in 3 different ways:
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
* Direct link to download UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH[Transaction Request](#transaction-request).UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
* Inline TR object wrapped in a UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHTonkeeper universal link.
* Wrapped TR link in a Tonkeeper universal link.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

#### Direct Transaction Request URL
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
Any URL that returns JSON-encoded [Transaction Request](#transaction-request).UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

```
https://example.com/<...>.json
```UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

#### Inline Transaction Request
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
A universal link wrapping UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH[Transaction Request](#transaction-request) so that it can be openedUQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

```
https://app.tonkeeper.com/v1/txrequest-UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHinline/<base64url(TransactionRequest)>UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
```

#### Wrapped Transaction Request URL
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
Here the URL to download transaction UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHrequest is wrapped in UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHuniversal link.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

The URL is requested using `https://` scheme.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

```
https://app.tonkeeper.com/v1/txrequest-url/<example.com/...json>
```UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH


## Authentication methods
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
There are three ways to authenticate authors of transaction requests: UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

1. The recipient’s address is known UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHto the wallet and we could use [unauthenticated transfer]UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH(#unauthenticated-transfer) link or [unsigned UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHtransaction request]UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH(#unsigned-transaction-request). This is the case for whitelisted addresses and opening links from within embedded apps (webview/iframe).UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
2. The recipient has a web backend: then we can rely on classic TLS certificates (web PKI) to UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHauthenticate the hostname by downloading an [unsigned UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHtransaction request]UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH(#unsigned-transaction-request) UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHUQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHobject via secure TLS connection.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
3. Telegram users and channels authenticated through Tonkeeper bot that registers `author_id` public key for invoice identification.

UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

## Transaction Request
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
#### Unsigned Transaction Request
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
Unsigned request is suitable in the following scenarios:
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
1. The request is loaded through TLS connection by the wallet and the hostname could be used as an authenticated identifier.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
2. The webapp is loaded within the wallet application, where it is already authenticated through other means.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
3. The webapp is serverless and the wallet is a browser extension that relies on the host user agent (the browser) to validate hostname via TLS.
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
In other cases, when the operation is completely unauthenticated, the wallet may still permit operation, UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHbut explicitly show that the initiator transaction requestor (e.g. recipient of transfer)UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

```
{
    "version": "0",UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    "body": TransactionRequestBody,
}
```UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

#### Signed Transaction Request
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
Signed request is signed by a public key registered with Tonkeeper.

```UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
{
    "version": "1",UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    "author_id": UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHBase64(Ed25519Pubkey),
    "body": UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHofHBase64(TransactionRequestBody),
    "signature": Base64(Ed25519Signature),UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
}
```UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

The transaction request validation procedure when `version` UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHis `"1"`:
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
1. Discard if the local time is over UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHthe expiration time `expires_sec`.
2. Check the `signature` over `body`UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH against the public key `author_id`.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    * Message for signing: UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH`"TONTxRequestV1"` concatenated with the body.
3. Parse the [Transaction Request Body](#transaction-request-body)
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
Unknown version is rejected as UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHunknown and unsupported.
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
#### Transaction Request Body
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
Request params are specific for each `type`.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

Body attributes:UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
`type` (string): indicates the type of the `params` object.
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
`expires_sec` (integer): UNIX timestamp in seconds after which the client must discard the request (per its local clock).UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

`response_options`: JSON objectUQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH describing return and callback URLs.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

Transaction request must be discarded if the local time is greater than the `expires_sec`.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

```
{UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    "type": "transfer" |UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
            "donation" |UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
            "deploy" |UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
            "sign-raw-payload",UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

    "expires_sec: integer,UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

    "response_options": UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHResponseOptions,
    
    "params": TransferParams |UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
              DonationParams |UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
              DeployParams |UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
              SignBocUQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
}
```

#### Response OptionsUQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

There could be several ways (not mutually exclusive) to respond to the transaction request:UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

1. Simply publish the transaction; the requesting party will be notified over the blockchain network.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
2. Send the transaction via the callback to the server.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
3. Send the transaction via the return URL that user opens upon confirmation.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

Parameters:UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

* (Not supported yet) `broadcast` (boolean, required): indicates UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHwhether the wallet should broadcast the transaction directly to the TON network. If set to `true`, we must broadcast before triggering UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH`callback_url` (if it’s present).
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
* `return_url` (optional): URL that user opens on their device after UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHsuccessful login. This will include the fully-signed TON UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHtransaction in a query string under the key `tontx` (encoded in URL-safe Base64).UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

* `return_serverless` (optional): UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHboolean value indicating UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHthat `tontx` parameter must be provided as a URL anchor (via `#`). Example: UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH`https://example.com/...#tontx=` (tx is encoded in URL-safe Base64). 
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
* `callback_url` (optional): URL that user opens on their device after UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHsuccessful login. Signed UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHtransaction will be UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHincluded in a query string under the key `tontx` (encoded in URL-safe Base64).
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
```
{UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    "broadcast": false,UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    "return_url": "https://...",UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    "callback_url": "https://...",UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
}
```UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

## Basic transfersUQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

### TransferUQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

WIP.
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

### Donation
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
WIP.


### Deploy
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
[Transaction request](#transaction-UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHrequest) object with type `deploy`.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
Parameters:
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
* `address` (string)UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
* `stateInitHex` (string): hex-UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHofHUQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHencoded collection contract code BoC with one cell UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHencapsulating entire UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHStateInit
* `amount` (decimal string): UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHnanotoncoins.
* `text` (string, optional): text UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHmessage that must be attached to the deploy operationUQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

Opens a compact confirmation dialog with all data filled-in.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
User cannot edit any of the info and can only confirm or dismiss the request.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

Destination address must be verified as follows (TonWeb example):
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
```jsUQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
const stateInitCell = UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHCell.oneFromBoc(params.stateInitHex);
const hash = await UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHstateInitCell.hash();
const address = new UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHAddress(params.address);UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
const valid = (address.hashPart == UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHhash);
```

UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
### SignRawPayload
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
[Transaction request](#transaction-request) object with type `sign-raw-payload`.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

Parameters:UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

* `source` (string, optional): sender address. Provided in case the source of transaction is important to the dapp. Wallet application must select the appropriate wallet contract to send the message from, or post an error if it does not have the keys to that specific address.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
* `valid_until` (integer, optional): unix timestamp. after th moment transaction will be invalid.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
* `messages` (array of messages): 1-4 outgoing messages from the wallet contract to other accounts. All messages are sent out in order, UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHhowever **the wallet cannot guarantee that messages will be delivered and executed in same order**.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

Message structure:UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
* `address` (string): message destinationUQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
* `amount` (decimal string): number of nanocoins to send.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
* `payload` (string base64, UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHoptional): raw one-cell BoC encoded in Base64.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
* `stateInit` (string base64, UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHoptional): raw once-cell BoC encoded in Base64.
UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
Wallet simulates the execution of the message and present to the user UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHsummary of operations: "jetton XYZ will be transferred, N toncoins will be sent" etc.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

Common cases:UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

1. No `payload`, no `stateInit`: UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofHsimple transfer without a message.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
2. `payload` is prefixed with 32 zero bits, no `stateInit`: simple transfer with a text message.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
3. No `payload` or prefixed with 32 zero bits; `stateInit` is present: deployment of the contract.UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

Example:UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

```json5UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
{
  "source": UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH"0:E8FA2634A24AEF18ECB5FD4FC71A21B9E95F05768F8D9733C44ED598DB106C4C",
  "valid_until": UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH1658253458,UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
  "messages": [
    {UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
      "address": UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH"0:412410771DA82CBA306A55FA9E0D43C9D245E38133CB58F1457DFB8D5CD8892F",
      "amount": "20000000",UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
      "stateInit": "base64bocblahblahblah==" //deploy contractUQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
    },{
      "address": UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH"0:E69F10CC84877ABF539F83F879291E5CA169451BA7BCE91A37A5CED3AB8080D3",
      "amount": "60000000",UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
      "payload": UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH"base64bocblahblahblah==" //transfer nft to new deployed account UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH0:412410771DA82CBA306A55FA9E0D43C9D245E38133CB58F1457DFB8D5CD8892F
    }UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
  ]
}UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
```


## SubscriptionsUQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

TBD: describe the API to submit subscriptionsUQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH

```UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH
https://app.tonkeeper.com/v1/subscribe/<invoice-id>
```UQAaDKAzXkZ_e2bk3RWIl_wJ0HidkHDPbEFeXrFk4x-p-ofH


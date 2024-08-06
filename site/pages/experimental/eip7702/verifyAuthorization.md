---
description: Verifies that an Authorization object was signed by the provided address.
---

# verifyAuthorization

Verifies that an Authorization object was signed by the provided address.

## Import

```ts twoslash
import { verifyAuthorization } from 'viem/experimental'
```

## Usage

:::code-group

```ts twoslash [example.ts]
import { verifyAuthorization } from 'viem/experimental' // [!code focus]
import { walletClient } from './client'

const authorization = await walletClient.signAuthorization({
  authorization: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2'
})

const valid = await verifyAuthorization({ // [!code focus]
  address: walletClient.account.address, // [!code focus]
  authorization, // [!code focus]
}) // [!code focus]
```

```ts twoslash [client.ts] filename="client.ts"
import { createWalletClient, http } from 'viem'
import { privateKeyToAccount } from 'viem/accounts'
import { mainnet } from 'viem/chains'
import { eip7702Actions } from 'viem/experimental'

export const walletClient = createWalletClient({
  account: privateKeyToAccount('0x...'),
  chain: mainnet,
  transport: http(),
}).extend(eip7702Actions())
```

:::

## Returns

`boolean`

Whether the signature is valid for the provided Authorization object.

## Parameters

### address

- **Type:** `Address`

The address that signed the Authorization object.

```ts twoslash
import { verifyAuthorization } from 'viem/experimental'
import { walletClient } from './client'

const authorization = await walletClient.signAuthorization({
  authorization: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2'
})
// ---cut---
const valid = await verifyAuthorization({
  address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48', // [!code focus]
  authorization,
}) 
```

### authorization

- **Type:** `Authorization | SignedAuthorization`

The Authorization object to be verified.

```ts twoslash
import { verifyAuthorization } from 'viem/experimental'
import { walletClient } from './client'
// ---cut---
const authorization = await walletClient.signAuthorization({
  authorization: '0xFBA3912Ca04dd458c843e2EE08967fC04f3579c2'
})

const valid = await verifyAuthorization({
  address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
  authorization, // [!code focus]
}) 
```

### signature

- **Type:** `Hex | ByteArray | Signature | SignedAuthorization`

The signature that was generated by signing the Authorization object with the address's private key.

```ts twoslash
import { verifyAuthorization } from 'viem/experimental'
import { walletClient } from './client'
// ---cut---
const signature = await walletClient.signAuthorization({
  authorization: {
    address: '0xd8da6bf26964af9d7eed9e03e53415d37aa96045',
    chainId: 1,
    nonce: 0,
  }
})

const valid = await verifyAuthorization({
  address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
  authorization: {
    address: '0xd8da6bf26964af9d7eed9e03e53415d37aa96045',
    chainId: 1,
    nonce: 0,
  },
  signature, // [!code focus]
}) 
```
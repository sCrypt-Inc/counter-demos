# counter-demos

![](https://aaron67-public.oss-cn-beijing.aliyuncs.com/202307151317201.png)

- [React](https://counter-react-pearl.vercel.app/)
- [Next.js](https://counter-next-psi.vercel.app/)
- [Angular](https://counter-angular-sigma.vercel.app/)
- [Svelte](https://counter-svelte-eight.vercel.app/)
- Vue 3.x
  - [bundled with Vite](https://counter-vue3-vite.vercel.app/)
  - [bundled with Webpack](https://counter-vue3-webpack.vercel.app/)
- Vue 2.x
  - [bundled with Vite](https://counter-vue2-vite.vercel.app/)
  - [bundled with Webpack](https://counter-vue2-webpack.vercel.app/)

## contract

```ts
import { method, prop, SmartContract, hash256, assert, ByteString, SigHash } from 'scrypt-ts'

export class Counter extends SmartContract {
    @prop(true)
    count: bigint

    constructor(count: bigint) {
        super(count)
        this.count = count
    }

    @method(SigHash.SINGLE)
    public increment() {
        this.count++

        // make sure balance in the contract does not change
        const amount: bigint = this.ctx.utxo.value
        // output containing the latest state
        const output: ByteString = this.buildStateOutput(amount)
        // verify current tx has this single output
        assert(this.ctx.hashOutputs === hash256(output), 'hashOutputs mismatch')
    }
}
```

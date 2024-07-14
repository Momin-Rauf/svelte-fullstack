<script lang="ts">
    import { PrivateKey } from '@bsv/sdk'
    
    let WIF:string
    let address:string
    
    function createKeys () {
    
        const privKey = PrivateKey.fromRandom()
        WIF = privKey.toWif()
        console.log("Private Key WIF format is ", WIF)
        address = privKey.toAddress()
        console.log("Your bitcoin address is ", address)
    }
    
    </script>
    
    <section class="flex flex-col gap-4 justify-center h-[100vh] items-center bg-slate-200" >
        <button class=" bg-black text-white p-2 rounded-full mx-auto" on:click={createKeys}> Generate New Wallet Keys </button>
        <p>Private Key WIF format is {WIF}</p>
        <p>Your BitCoin Address is {address}</p>
    </section>
    
    
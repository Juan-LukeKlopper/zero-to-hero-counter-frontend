<script>
	import welcome from '$lib/images/svelte-welcome.webp';
	import welcome_fallback from '$lib/images/svelte-welcome.png'; 
    
    import { SecretNetworkClient } from "secretjs";

    const CHAIN_ID = "pulsar-3";
    const LCD_URL = "https://api.pulsar3.scrttestnet.com";

    const contractAddress = "secret1mchalhcf7k9ermg0sq7jwlxsvncdnx58zkffd5";
    const codeHash = "3c15a66ba05b34a1a9218a3a3c1f77bb7f22309fcc6f6d753d84f4ebf7e47014";


    let secretjs = new SecretNetworkClient({
        url: LCD_URL,
        chainId: CHAIN_ID,
    });
    let wallet_address;
    let connected = false;

    async function setupKeplr() {
        await window.keplr.enable(CHAIN_ID);
        window.keplr.defaultOptions = {
          sign: {
            preferNoSetFee: false,
            disableBalanceCheck: true,
          },
        };

        const keplrOfflineSigner = window.getOfflineSignerOnlyAmino(CHAIN_ID);
        const accounts = await keplrOfflineSigner.getAccounts();

        wallet_address = accounts[0].address;
        secretjs = new SecretNetworkClient({
            chainId: CHAIN_ID,
            url: LCD_URL,
            wallet: keplrOfflineSigner,
            walletAddress: wallet_address,
            encryptionUtils: window.getEnigmaUtils(CHAIN_ID),
        });
        connected = true;
    }

    async function connectWallet() {
        try {
            if (!window.keplr) {
                console.log("intall keplr!");
            } else {
                await setupKeplr();
                localStorage.setItem("keplrAutoConnect", "true");
            }
        } catch (error) {
            alert(
                "An error occurred while connecting to the wallet. Please try again."
            );
        }
    }


    // Query messages of the contract
    let query_count = async () => {
        let my_query = await secretjs.query.compute.queryContract({
            contract_address: contractAddress,
            code_hash: codeHash,
            query: { get_count: {} },
        });
        alert(JSON.stringify(my_query));
    };

    let query_x_factor = async () => {
        let my_query = await secretjs.query.compute.queryContract({
            contract_address: contractAddress,
            code_hash: codeHash,
            query: { get_x_factor: {} },
        });
        alert(JSON.stringify(my_query));
    };

    let query_club_count = async () => {
        let my_query = await secretjs.query.compute.queryContract({
            contract_address: contractAddress,
            code_hash: codeHash,
            query: { get_members_only_count: {} },
        });
        alert(JSON.stringify(my_query));
    };
    
    let query_club_members = async () => {
        let my_query = await secretjs.query.compute.queryContract({
            contract_address: contractAddress,
            code_hash: codeHash,
            query: { get_member_list: {} },
        });
        alert(JSON.stringify(my_query));
    };

    let query_waiting_list = async () => {
        let my_query = await secretjs.query.compute.queryContract({
            contract_address: contractAddress,
            code_hash: codeHash,
            query: { get_waiting_list: {} },
        });
        alert(JSON.stringify(my_query));
    };


    // Execute messages of the contract

    let try_execute_increment = async () => {
        const tx = await secretjs.tx.compute.executeContract({
            sender: wallet_address,
            contract_address: contractAddress,
            msg: {
                increment: {},
            },
            code_hash: codeHash,
            },
            { gasLimit: 100_000 }
        );
        console.log(tx);
        alert(JSON.stringify(tx));
    };


    let try_execute_increment_x_factor = async () => {
        const tx = await secretjs.tx.compute.executeContract({
            sender: wallet_address,
            contract_address: contractAddress,
            msg: {
                increment_x_factor: {},
            },
            code_hash: codeHash,
            },
            { gasLimit: 100_000 }
        );
        console.log(tx);
        alert(JSON.stringify(tx));
    };

    let try_execute_increment_club_count = async () => {
        const tx = await secretjs.tx.compute.executeContract({
            sender: wallet_address,
            contract_address: contractAddress,
            msg: {
                increment_members_only_count: {},
            },
            code_hash: codeHash,
            },
            { gasLimit: 100_000 }
        );
        console.log(tx);
        alert(JSON.stringify(tx));
    };

    let try_execute_increment_randomly = async () => {
        const tx = await secretjs.tx.compute.executeContract({
            sender: wallet_address,
            contract_address: contractAddress,
            msg: {
                increment_count_by_random_amount: {},
            },
            code_hash: codeHash,
            },
            { gasLimit: 100_000 }
        );
        console.log(tx);
        alert(JSON.stringify(tx));
    };

    let try_execute_add_to_waiting_list = async () => {
        const tx = await secretjs.tx.compute.executeContract({
            sender: wallet_address,
            contract_address: contractAddress,
            msg: {
                add_me_to_waiting_list: {},
            },
            code_hash: codeHash,
            },
            { gasLimit: 100_000 }
        );
        console.log(tx);
        alert(JSON.stringify(tx));
    };


    let try_execute_add_waiting_list_to_club = async () => {
        const tx = await secretjs.tx.compute.executeContract({
            sender: wallet_address,
            contract_address: contractAddress,
            msg: {
                add_waiting_list_to_club: {},
            },
            code_hash: codeHash,
            },
            { gasLimit: 100_000 }
        );
        console.log(tx);
        alert(JSON.stringify(tx));
    };

    let try_execute_add_member_to_club = async (address) => {
        const tx = await secretjs.tx.compute.executeContract({
            sender: wallet_address,
            contract_address: contractAddress,
            msg: {
                add_member_to_club: {prospect: address},
            },
            code_hash: codeHash,
            },
            { gasLimit: 100_000 }
        );
        console.log(tx);
        alert(JSON.stringify(tx));
    };

    let try_execute_reset_count = async () => {
        const tx = await secretjs.tx.compute.executeContract({
            sender: wallet_address,
            contract_address: contractAddress,
            msg: {
                reset: {count: 0},
            },
            code_hash: codeHash,
            },
            { gasLimit: 100_000 }
        );
        console.log(tx);
        alert(JSON.stringify(tx));
    };

    let try_execute_reset_x_factor = async () => {
        const tx = await secretjs.tx.compute.executeContract({
            sender: wallet_address,
            contract_address: contractAddress,
            msg: {
                reset_x_factor: {x_factor: 0},
            },
            code_hash: codeHash,
            },
            { gasLimit: 100_000 }
        );
        console.log(tx);
        alert(JSON.stringify(tx));
    };


    let try_execute_reset_members_only_count = async () => {
        const tx = await secretjs.tx.compute.executeContract({
            sender: wallet_address,
            contract_address: contractAddress,
            msg: {
                reset_members_only_count: {},
            },
            code_hash: codeHash,
            },
            { gasLimit: 100_000 }
        );
        console.log(tx);
        alert(JSON.stringify(tx));
    };


    let try_execute_randomise_x_factor = async () => {
        const tx = await secretjs.tx.compute.executeContract({
            sender: wallet_address,
            contract_address: contractAddress,
            msg: {
                randomise_x_factor: {},
            },
            code_hash: codeHash,
            },
            { gasLimit: 100_000 }
        );
        console.log(tx);
        alert(JSON.stringify(tx));
    };





</script>

<svelte:head>
	<title>Home</title>
	<meta name="Zero to hero counter contract frontend" content="A small and simple interface to a custom counter contract that has been deployed onto the secret network pulsar-3 testnet" />
</svelte:head>

<section>
	<h1>
		<span class="welcome">
			<picture>
				<source srcset={welcome} type="image/webp" />
				<img src={welcome_fallback} alt="Welcome" />
			</picture>
		</span>

		to the zero to hero <br> counter contract
	</h1>

    {#if !connected}
	    <button class="button" on:click={connectWallet}>
            Connect Keplr
        </button>
    {:else}
        <div class="container">
            <h1> 
                Query messages:
            </h1>
            <button class="button" on:click={query_count}>
	            Click on me to reveal count
            </button>
            <button  class="button" on:click={query_x_factor}>
	            Click on me to reveal x factor
            </button>
            <button  class="button" on:click={query_club_count}>
	            Click on me to reveal members only count
            </button>
            <button  class="button" on:click={query_waiting_list}>
	            Click on me to reveal waiting list
            </button>
            <button  class="button" on:click={query_club_members}>
	            Click on me to reveal members list
            </button>
        </div>
        <div class="container">
            <h1> 
                Execute messages:
            </h1>
            <button class="button" on:click={try_execute_increment}>
	            Click on me to increment count
            </button>
            <button class="button" on:click={try_execute_increment_randomly}>
	            Click on me to increment count with a random amount
            </button>
            <button  class="button" on:click={try_execute_increment_x_factor}>
	            Click on me to increment x factor
            </button>
            <button  class="button" on:click={try_execute_add_to_waiting_list}>
	            Click on me to add yourself to the waiting list
            </button>
        </div>
        <div class="container">
            <h2> 
                These will only work if you have an x in your address
            </h2>
            <button  class="button" on:click={try_execute_increment_x_factor}>
	            Click on me to increment x factor
            </button>
            <button  class="button" on:click={try_execute_reset_x_factor}>
	            Click on me to reset x factor
            </button>
            <button  class="button" on:click={try_execute_randomise_x_factor}>
	            Click on me to randomise x factor
            </button>
        </div>
        <div class="container">
            <h2> 
                These will only work if you are part of the members club
            </h2>
            <button class="button" on:click={try_execute_increment_club_count}>
	            Click on me to increment members only count
            </button>
            <button class="button" on:click={try_execute_add_waiting_list_to_club}>
	            Click on me to add waiting list to club
            </button>
            <button  class="button" on:click={try_execute_reset_count}>
	            Click on me to reset count
            </button>
            <button  class="button" on:click={try_execute_reset_members_only_count}>
	            Click on me to reset members only count
            </button>
        </div>

    {/if}

</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}

    .container {
        border: 5px solid #541a0f;
        display: flex;
        flex-direction: column;
        padding: 15px;
        margin: 15px;
        border-radius: 15px;
    }

	h1 {
		width: 100%;
	}

    h2 {
        width: 100%;
        font-size: 30px;
    }

	.welcome {
		display: block;
		position: relative;
		width: 100%;
		height: 0;
		padding: 0 0 calc(100% * 495 / 2048) 0;
	}

	.welcome img {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		display: block;
	}
 
    .button {
        align-items: center;
        appearance: none;
        background-clip: padding-box;
        background-color: initial;
        background-image: none;
        border-style: none;
        box-sizing: border-box;
        color: #fff;
        cursor: pointer;
        display: inline-block;
        flex-direction: row;
        flex-shrink: 0;
        font-family: Eina01,sans-serif;
        font-size: 16px;
        font-weight: 800;
        justify-content: center;
        line-height: 24px;
        margin: 10px;
        min-height: 64px;
        outline: none;
        overflow: visible;
        padding: 19px 26px;
        pointer-events: auto;
        position: relative;
        text-align: center;
        text-decoration: none;
        text-transform: none;
        user-select: none;
        -webkit-user-select: none;
        touch-action: manipulation;
        vertical-align: middle;
        width: auto;
        word-break: keep-all;
        z-index: 0;
    }

    @media (min-width: 768px) {
        .button {
            padding: 19px 32px;
        }
    }

    .button:before,
    .button:after {
        border-radius: 80px;
    }

    .button:before {
        background-image: linear-gradient(92.83deg, #ff7426 0, #f93a13 100%);
        content: "";
        display: block;
        height: 100%;
        left: 0;
        overflow: hidden;
        position: absolute;
        top: 0;
        width: 100%;
        z-index: -2;
    }

    .button:after {
        background-color: initial;
        background-image: linear-gradient(#541a0f 0, #0c0d0d 100%);
        bottom: 4px;
        content: "";
        display: block;
        left: 4px;
        overflow: hidden;
        position: absolute;
        right: 4px;
        top: 4px;
        transition: all 100ms ease-out;
        z-index: -1;
    }

    .button:hover:not(:disabled):before {
        background: linear-gradient(92.83deg, rgb(255, 116, 38) 0%, rgb(249, 58, 19) 100%);
    }

    .button:hover:not(:disabled):after {
        bottom: 0;
        left: 0;
        right: 0;
        top: 0;
        transition-timing-function: ease-in;
        opacity: 0;
    }

    .button:active:not(:disabled) {
        color: #ccc;
    }

    .button:active:not(:disabled):before {
        background-image: linear-gradient(0deg, rgba(0, 0, 0, .2), rgba(0, 0, 0, .2)), linear-gradient(92.83deg, #ff7426 0, #f93a13 100%);
    }

    .button:active:not(:disabled):after {
        background-image: linear-gradient(#541a0f 0, #0c0d0d 100%);
        bottom: 4px;
        left: 4px;
        right: 4px;
        top: 4px;
    }

    .button:disabled {
        cursor: default;
        opacity: .24;
    }
</style>

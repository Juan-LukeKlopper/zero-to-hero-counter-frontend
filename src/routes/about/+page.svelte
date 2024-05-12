<script>
    let contract_address = "secret1mchalhcf7k9ermg0sq7jwlxsvncdnx58zkffd5"
</script>

<svelte:head>
	<title>About</title>
	<meta name="description" content="About this app" />
</svelte:head>

<div class="text-column">
	<h1>About this app</h1>

	<p>
		This is a <a href="https://kit.svelte.dev">SvelteKit</a> app which can interact with my basic Zero-to-hero counter contract
	</p>

	<p>
        This contract features a Members list, this is a list of cool addresses that are allowed to reset counters and add other addresses to the list, a Waiting list where individuals can express interest to join the members list, and 3 counters: first is count which is a counter anyone can increment, x factor which is a counter only users whos address contain a X can increment and member only count which as the name suggest can only be incremented by members. 
	</p>

	<p>
		In addition to exploring the website, you can interact with the smart contract directly using the command-line interface (CLI) commands.
    </p>
    

    <h3>
        Query Messages:
    </h3>

    <ul>
        <li>
            <strong>Get Count: </strong> Retrieve the current count from the smart contract.
            <br><br>
            <code>
                secretcli query compute query {contract_address} {`'{"get_count": {}}'`}
            </code>
            <br><br>
        </li>
        <li>
            <strong>Get X Factor: </strong> Retrieve the current x factor from the smart contract.
            <br><br>
            <code>
                secretcli query compute query {contract_address} {`'{"get_x_factor": {}}'`} 
            </code>
            <br><br>
        </li>
        <li> 
            <strong>Get Waiting List: </strong> Retrieve the current address on the waiting list from the smart contract.
            <br><br>
            <code>
                secretcli query compute query {contract_address} {`'{"get_waiting_list": {}}'`}
            </code>
            <br><br>
        </li>
        <li> 
            <strong>Get Members List: </strong> Retrieve the current members/admin list from the smart contract.
            <br><br>
            <code>
                secretcli query compute query {contract_address} {`'{"get_members_list": {}}'`}
            </code>
            <br><br>
        </li>
    </ul>
	
    <h3>
        Execution Messages:
    </h3>

    <ul>
        <li>
            <strong>Increment Count: </strong> add one to the current count from the smart contract.
            <br><br>
            <code>
                secretcli tx compute execute {contract_address} {`'{"increment": {}}'`}
            </code>
            <br><br>
        </li>
        <li>
            <strong>Increment Count Randomly: </strong> add a random number to the current count from the smart contract.
            <br><br>
            <code>
                secretcli tx compute execute {contract_address} {`'{"increment_count_by_random_amount": {}}'`}
            </code>
            <br><br>
        </li>
        <li>
            <strong>Increment X Factor: </strong> add one the current x factor from the smart contract.
            <br><br>
            <code>
                secretcli tx compute execute {contract_address} {`'{"increment_x_factor": {}}'`} 
            </code>
            <br><br>
        </li>
        <li> 
            <strong>Add Me to Waiting List: </strong> add the senders address on to the waiting list from the smart contract.
            <br><br>
            <code>
                secretcli tx compute execute {contract_address} {`'{"add_me_to_waiting_list": {}}'`}
            </code>
            <br><br>
        </li>
    </ul>

    <h3>
        Execution Messages(for members only):
    </h3>

    <ul>
        <li>
            <strong>Add Member to Club: </strong> add an address to the members list of the smart contract.
            <br>**Note!** please replace example address with the secret network address you want to add 
            <br><br>
            <code>
                secretcli tx compute execute {contract_address} {`'{"add_member_to_club": {"prospect" : "secret1xndlc..."}}'`}
            </code>
            <br><br>
        </li>
        <li>
            <strong>Add Waiting List to Club: </strong> add all address on the waiting list to the members list of  thesmart contract.
            <br><br>
            <code>
                secretcli tx compute execute {contract_address} {`'{"add_waiting_list_to_club": {}}'`} 
            </code>
            <br><br>
        </li>
        <li> 
            <strong>Reset: </strong> reset the count's state on the smart contract.
            <br><br>
            <code>
                secretcli tx compute execute {contract_address} {`'{"reset": {"count": 0}}'`}
            </code>
            <br><br>
        </li>
        <li> 
            <strong>Reset X Factor: </strong> reset the x factor's state on the smart contract.
            <br><br>
            <code>
                secretcli tx compute execute {contract_address} {`'{"reset_x_factor": {"x_factor": 0}}'`}
            </code>
            <br><br>
        </li>
        <li> 
            <strong>Reset Member Only Count: </strong> reset the members only count's state on the smart contract.
            <br><br>
            <code>
                secretcli tx compute execute {contract_address} {`'{"reset_members_only_count": {}}'`}
            </code>
            <br><br>
        </li>

    </ul>

</div>

<style>
    li {
        white-space: nowrap;
    }

    code {
        border-spacing: 10px;
        border: var(--color-theme-1);
        border-width: 1px;
        border-style: solid;
        margin: 1px;
        padding: 5px;
    }
</style>

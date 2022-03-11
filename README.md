# My-First-DApp
//i created my first decentralised app.
//here is my code in VSCode.
<html>
    <body>
        <h1>this is raphael's first dApp.</h1>
        <p>here we are going to set up your mood.</p>
        <label for="mood">Input </label>
        <input type="text" id="'mood" />
        <div>
            <button onclick="getMood()">Get Mood</button>
        </div>
        <div>
            <button onclick="setMood()">Set Mood</button>
        </div>
    </body>
    <script 
        charset="utf-8"
        src="https://cdn.ethers.io/scripts/ethers-v4.min.js"
        type="text/javascript"
    ></script>
    <script>
        window.ethereum.enable();
        var provider = new ethers.providers.Web3Provider(
            window.ethereum,"ropsten"
        );
        var MoodContractAddress = "0xA83808Ec5E2Ec6C0f02B2F67d975FE26df1b3e24"
        var MoodContractABI = [
	{
		"inputs": [],
		"name": "getMood",
		"outputs": [
			{
				"internalType": "string",
				"name": "",
				"type": "string"
			}
		],
		"stateMutability": "view",
		"type": "function"
	},
	{
		"inputs": [
			{
				"internalType": "string",
				"name": "_mood",
				"type": "string"
			}
		],
		"name": "setMood",
		"outputs": [],
		"stateMutability": "nonpayable",
		"type": "function"
	},
]
        var MoodContract;
        var signer;
        provider.listAccounts().then(function(accounts) {
            signer = provider.getSigner(accounts[0]);
            MoodContract = new ethers.Contract(
                MoodContractAddress,
                MoodContractABI,
                signer
            );
        });
        async function getMood(){
            getMoodPromise = MoodContract.getMood();
            var Mood = await getMoodPromise;
            console.log(Mood);
        }
        async function setMood(){
            let mood = document.getElementById("mood").value;
            setMoodPromise = MoodContract.setMood(mood);
            await setMoodPromise;
        }
    </script>
</html>

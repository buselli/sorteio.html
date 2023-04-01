<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sorteio de Prêmios</title>
    <script src="https://cdn.ethers.io/lib/ethers-5.0.umd.min.js" type="application/javascript"></script>
</head>
<body>
    <h1>Sorteio de Prêmios</h1>
    <button id="connect">Conectar Carteira</button>
    <button id="createRaffle">Criar Sorteio</button>
    <br>
    <label for="raffleId">ID do Sorteio:</label>
    <input type="text" id="raffleId">
    <button id="buyTicket">Comprar Bilhete</button>
    <br>
    <label for="winningTicket">Bilhete Vencedor:</label>
    <input type="text" id="winningTicket">
    <button id="endRaffle">Encerrar Sorteio</button>
    <br>
    <div id="output"></div>

    <script>
        // Substitua com o ABI do seu contrato
        const contractABI = [
	{
		"inputs": [
			{
				"internalType": "contract IERC20",
				"name": "_token",
				"type": "address"
			},
			{
				"internalType": "uint256",
				"name": "_precoBilhete",
				"type": "uint256"
			}
		],
		"stateMutability": "nonpayable",
		"type": "constructor"
	},
	{
		"anonymous": false,
		"inputs": [
			{
				"indexed": false,
				"internalType": "uint256",
				"name": "idSorteio",
				"type": "uint256"
			},
			{
				"indexed": false,
				"internalType": "uint256",
				"name": "idBilhete",
				"type": "uint256"
			},
			{
				"indexed": false,
				"internalType": "address",
				"name": "comprador",
				"type": "address"
			}
		],
		"name": "BilheteComprado",
		"type": "event"
	},
	{
		"inputs": [
			{
				"internalType": "uint256",
				"name": "idSorteio",
				"type": "uint256"
			},
			{
				"internalType": "address",
				"name": "enderecoRecebimento",
				"type": "address"
			}
		],
		"name": "comprarBilhete",
		"outputs": [],
		"stateMutability": "nonpayable",
		"type": "function"
	},
	{
		"inputs": [
			{
				"internalType": "uint256",
				"name": "idSorteio",
				"type": "uint256"
			},
			{
				"internalType": "uint256",
				"name": "bilheteVencedor",
				"type": "uint256"
			}
		],
		"name": "concluirSorteio",
		"outputs": [],
		"stateMutability": "nonpayable",
		"type": "function"
	},
	{
		"inputs": [],
		"name": "criarSorteio",
		"outputs": [],
		"stateMutability": "nonpayable",
		"type": "function"
	},
	{
		"inputs": [
			{
				"internalType": "uint256",
				"name": "novoPreco",
				"type": "uint256"
			}
		],
		"name": "mudarPrecoBilhete",
		"outputs": [],
		"stateMutability": "nonpayable",
		"type": "function"
	},
	{
		"anonymous": false,
		"inputs": [
			{
				"indexed": false,
				"internalType": "uint256",
				"name": "idSorteio",
				"type": "uint256"
			},
			{
				"indexed": false,
				"internalType": "uint256",
				"name": "bilheteVencedor",
				"type": "uint256"
			},
			{
				"indexed": false,
				"internalType": "address",
				"name": "ganhador",
				"type": "address"
			}
		],
		"name": "SorteioConcluido",
		"type": "event"
	},
	{
		"anonymous": false,
		"inputs": [
			{
				"indexed": false,
				"internalType": "uint256",
				"name": "id",
				"type": "uint256"
			},
			{
				"indexed": false,
				"internalType": "uint256",
				"name": "timestamp",
				"type": "uint256"
			}
		],
		"name": "SorteioCriado",
		"type": "event"
	},
	{
		"inputs": [],
		"name": "administrador",
		"outputs": [
			{
				"internalType": "address",
				"name": "",
				"type": "address"
			}
		],
		"stateMutability": "view",
		"type": "function"
	},
	{
		"inputs": [
			{
				"internalType": "uint256",
				"name": "",
				"type": "uint256"
			},
			{
				"internalType": "uint256",
				"name": "",
				"type": "uint256"
			}
		],
		"name": "bilhetes",
		"outputs": [
			{
				"internalType": "address",
				"name": "",
				"type": "address"
			}
		],
		"stateMutability": "view",
		"type": "function"
	},
	{
		"inputs": [
			{
				"internalType": "uint256",
				"name": "idSorteio",
				"type": "uint256"
			},
			{
				"internalType": "uint256",
				"name": "idBilhete",
				"type": "uint256"
			}
		],
		"name": "getBilhete",
		"outputs": [
			{
				"internalType": "address",
				"name": "",
				"type": "address"
			}
		],
		"stateMutability": "view",
		"type": "function"
	},
	{
		"inputs": [],
		"name": "getNumeroSorteios",
		"outputs": [
			{
				"internalType": "uint256",
				"name": "",
				"type": "uint256"
			}
		],
		"stateMutability": "view",
		"type": "function"
	},
	{
		"inputs": [
			{
				"internalType": "uint256",
				"name": "idSorteio",
				"type": "uint256"
			}
		],
		"name": "getSorteio",
		"outputs": [
			{
				"components": [
					{
						"internalType": "uint256",
						"name": "id",
						"type": "uint256"
					},
					{
						"internalType": "uint256",
						"name": "timestamp",
						"type": "uint256"
					},
					{
						"internalType": "uint256",
						"name": "premioTotal",
						"type": "uint256"
					},
					{
						"internalType": "uint256",
						"name": "numeroBilhetes",
						"type": "uint256"
					},
					{
						"internalType": "uint256",
						"name": "bilheteVencedor",
						"type": "uint256"
					},
					{
						"internalType": "bool",
						"name": "concluido",
						"type": "bool"
					}
				],
				"internalType": "struct SorteioPremios.Sorteio",
				"name": "",
				"type": "tuple"
			}
		],
		"stateMutability": "view",
		"type": "function"
	},
	{
		"inputs": [],
		"name": "precoBilhete",
		"outputs": [
			{
				"internalType": "uint256",
				"name": "",
				"type": "uint256"
			}
		],
		"stateMutability": "view",
		"type": "function"
	},
	{
		"inputs": [
			{
				"internalType": "uint256",
				"name": "",
				"type": "uint256"
			}
		],
		"name": "sorteios",
		"outputs": [
			{
				"internalType": "uint256",
				"name": "id",
				"type": "uint256"
			},
			{
				"internalType": "uint256",
				"name": "timestamp",
				"type": "uint256"
			},
			{
				"internalType": "uint256",
				"name": "premioTotal",
				"type": "uint256"
			},
			{
				"internalType": "uint256",
				"name": "numeroBilhetes",
				"type": "uint256"
			},
			{
				"internalType": "uint256",
				"name": "bilheteVencedor",
				"type": "uint256"
			},
			{
				"internalType": "bool",
				"name": "concluido",
				"type": "bool"
			}
		],
		"stateMutability": "view",
		"type": "function"
	},
	{
		"inputs": [],
		"name": "token",
		"outputs": [
			{
				"internalType": "contract IERC20",
				"name": "",
				"type": "address"
			}
		],
		"stateMutability": "view",
		"type": "function"
	}
];

        // Substitua com o endereço do seu contrato
        const contractAddress = "0x98A739de957cD0765759E1eFc172C6f448085Ba0x";

        let provider;
        let signer;
        let contract;

        async function checkMetaMask() {
            if (typeof window.ethereum !== "undefined" && window.ethereum.isMetaMask) {
                return true;
            }
            return false;
        }

        async function connectWallet() {
            if (await checkMetaMask()) {
                provider = new ethers.providers.Web3Provider(window.ethereum);
                signer = provider.getSigner();
                contract = new ethers.Contract(contractAddress, contractABI, signer);

                try {
                    await window.ethereum.enable();
                    const accounts = await provider.listAccounts();
                    const userAddress = accounts[0];

                    document.getElementById("output").innerHTML = "Carteira conectada: " + userAddress;
                } catch (error) {
                    document.getElementById("output").innerHTML = "Erro ao conectar carteira.";
                }
            } else {
                document.getElementById("output").innerHTML = "Por favor, instale MetaMask!";
            }
        }

        // Restante do código...
    </script>
</body>
</html>

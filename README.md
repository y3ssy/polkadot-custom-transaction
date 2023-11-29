# polkadot-custom-transaction    
By utilizing the Substrate API, users can define and execute custom transactions, exploring the flexibility and extensibility of the Polkadot network. 
from substrateinterface import SubstrateInterface, Keypair

class PolkadotCustomTransactionScript:
    def __init__(self, node_url, keypair):
        self.substrate = SubstrateInterface(url=node_url)
        self.keypair = keypair

    def custom_transaction(self, module, function, params):
        # Submit a custom transaction to the Polkadot blockchain
        call = self.substrate.compose_call(call_module=module, call_function=function, call_params=params)
        extrinsic = self.substrate.create_signed_extrinsic(call=call, keypair=self.keypair)
        self.substrate.submit_extrinsic(extrinsic, wait_for_inclusion=True)
        print(f"Custom transaction submitted: {module}.{function} with parameters {params}")

# Example Usage
node_url = "wss://rpc.polkadot.io"
alice_keypair = Keypair.create_from_mnemonic("your_alice_mnemonic_here")

polkadot_custom_script = PolkadotCustomTransactionScript(node_url, alice_keypair)

# Submit a custom transaction (example: transfer to another account)
transaction_params = {'dest': 'recipient_address_here', 'value': 20}
polkadot_custom_script.custom_transaction('Balances', 'transfer', transaction_params)

This script empowers developers to execute custom transactions on the Polkadot blockchain. By defining the module, function, and parameters, users can tailor transactions to their specific needs. This script serves as a versatile tool for exploring and integrating custom functionality into the Polkadot network.

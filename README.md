# op-rollups







Steps:
1. Build the Optimism monorepo
    ```
    cd ~
    git clone https://github.com/ethereum-optimism/optimism.git

    cd optimism
    git checkout tutorials/chain

    #check depencencies
    ./packages/contracts-bedrock/scripts/getting-started/versions.sh

    pnpm install

    #if you come accross sort of issue with make file
    #better downgrade your go version to 1.21.7
    
    make op-node op-batcher op-proposer
    pnpm build
    ```
2. Build `op-geth`
    ```
    cd ~
    git clone https://github.com/ethereum-optimism/op-geth.git

    cd op-geth

    make geth
    ```

3. Fill out environment variables
     ```
     cd ~/optimism

     cp .envrc.example .envrc

     #Fill out the environment variable file

     `L1_RPC_URL` - URL for your L1 node
     `L1_RPC_KIND` - Kind of L1 RPC you're connecting to, used to inform optimal transactions receipts fetching. Valid options: alchemy, quicknode, infura, parity, nethermind, debug_geth,
     erigon, basic, any.
     ```
4. Generate Addresses
     ```
     cd ~/optimism
      #do not use this in production
     ./packages/contracts-bedrock/scripts/getting-started/wallets.sh

     #you should seee the outpust as Admin address, batcher Address, Praposer Address, Sequencer Address
     #save the addresses in .envrc

     #Fund the addresses Admin address 0.5 eth, batcher Address 0.1 eth, Praposer Address 0.2 Eth
     ```
5. Load environment variables
     ```
     cd ~/optimism
     direnv allow
     #outputs ->
     direnv: loading ~/optimism/.envrc                                                            
     direnv: export +DEPLOYMENT_CONTEXT +ETHERSCAN_API_KEY +GS_ADMIN_ADDRESS +GS_ADMIN_PRIVATE_KEY +GS_BATCHER_ADDRESS +GS_BATCHER_PRIVATE_KEY +GS_PROPOSER_ADDRESS +GS_PROPOSER_PRIVATE_KEY +GS_SEQUENCER_ADDRESS +GS_SEQUENCER_PRIVATE_KEY +IMPL_SALT +L1_RPC_KIND +L1_RPC_URL +PRIVATE_KEY +TENDERLY_PROJECT +TENDERLY_USERNAME
     ```
6. Configure your network
   
     ```
     cd ~/optimism
     cd packages/contracts-bedrock

     forge install

     ./scripts/getting-started/config.sh
     
     ```
8. Deploy the L1 contract
    ```
       forge script scripts/Deploy.s.sol:Deploy --private-key $GS_ADMIN_PRIVATE_KEY --broadcast --rpc-url $L1_RPC_URL --slow
    ```    
   
 


```cast send <TO ADDRESS> --value 2 --private-key [FROM_PK] --rpc-url http://127.0.0.1:8545```

     

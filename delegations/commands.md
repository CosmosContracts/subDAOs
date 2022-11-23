# Delegations SubDAO Creation Proposal

This gist breaks down and explains the Delegations SubDAO instantiation message.

For context, the instantiation message creates a new smart contract. In DAO DAO, the instantiation message actually creates multiple smart contracts that constitute the DAO.

## Proposal module instantiate message

The proposal module contains the settings for voting and execution of proposals.

Revoting is allowed, meaning members can change their votes up until the proposal has passed if they have recieved new information. For a proposal to pass, 6 / 11 members must vote YES. The voting period is 5 days.

Only members of the SubDAO can execute a proposal once it is passed.

```json
{"allow_revoting":true,"max_voting_period":{"time":604800},"only_members_execute":true,"threshold":{"absolute_count":{"threshold":"5"}}}
```

Encoded as base64 (which you can verify using a base64 decoder like [this one](https://www.base64decode.org/)):

```
eyJhbGxvd19yZXZvdGluZyI6dHJ1ZSwibWF4X3ZvdGluZ19wZXJpb2QiOnsidGltZSI6NjA0ODAwfSwib25seV9tZW1iZXJzX2V4ZWN1dGUiOnRydWUsInRocmVzaG9sZCI6eyJhYnNvbHV0ZV9jb3VudCI6eyJ0aHJlc2hvbGQiOiI1In19fQ==
```

## Voting module instantiate message

The voting module determins who has voting power in the DAO. In this case, this list is managed by a `cw4-groups` contract. Each member of the Juno Growth Fund SubDAO has submitted their addresses, and will each have a voting power of 1.

```json
{
  "cw4_group_code_id": 434,
  "initial_members": [
    {
      "addr": "juno1s33zct2zhhaf60x4a90cpe9yquw99jj0zen8pt",
      "weight": 1
    },
    {
      "addr": "juno18qw9ydpewh405w4lvmuhlg9gtaep79vy2gmtr2",
      "weight": 1
    },
    {
      "addr": "juno19mxp5ye8es3n5p08xkxg2ql90a8fw6jeufmuf6",
      "weight": 1
    },
    {
      "addr": "juno18r7ud9plhxx90shsz2cnahhqfsfmhcuhaxsuqz",
      "weight": 1
    },
    {
      "addr": "juno1znsn0qfvjstcahvlv62s69xx9lrt7sfdrqewyp",
      "weight": 1
    },
    {
      "addr": "juno1uss8lufa97pmd7ezlsvtnqcmmwqwxkd0wthgfg",
      "weight": 1
    },
    {
      "addr": "juno1sl5udxmndh7x99v2p32lt34jchjyexm76t497m",
      "weight": 1
    },
    {
      "addr": "juno1wt29e7ec5f04xy6ez5m6agzrweh0vxsu3ucc55",
      "weight": 1
    },
    {
      "addr": "juno1eck27qefttt5twxsg38gsr0q0hr4e3vvyxm2q4",
      "weight": 1
    }
  ]
}
```

Encoded as base64 (which you can verify using a base64 decoder like [this one](https://www.base64decode.org/)):

```
ewogICJjdzRfZ3JvdXBfY29kZV9pZCI6IDQzNCwKICAiaW5pdGlhbF9tZW1iZXJzIjogWwogICAgewogICAgICAiYWRkciI6ICJqdW5vMXMzM3pjdDJ6aGhhZjYweDRhOTBjcGU5eXF1dzk5amowemVuOHB0IiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xOHF3OXlkcGV3aDQwNXc0bHZtdWhsZzlndGFlcDc5dnkyZ210cjIiLAogICAgICAid2VpZ2h0IjogMQogICAgfSwKICAgIHsKICAgICAgImFkZHIiOiAianVubzE5bXhwNXllOGVzM241cDA4eGt4ZzJxbDkwYThmdzZqZXVmbXVmNiIsCiAgICAgICJ3ZWlnaHQiOiAxCiAgICB9LAogICAgewogICAgICAiYWRkciI6ICJqdW5vMThyN3VkOXBsaHh4OTBzaHN6MmNuYWhocWZzZm1oY3VoYXhzdXF6IiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xem5zbjBxZnZqc3RjYWh2bHY2MnM2OXh4OWxydDdzZmRycWV3eXAiLAogICAgICAid2VpZ2h0IjogMQogICAgfSwKICAgIHsKICAgICAgImFkZHIiOiAianVubzF1c3M4bHVmYTk3cG1kN2V6bHN2dG5xY21td3F3eGtkMHd0aGdmZyIsCiAgICAgICJ3ZWlnaHQiOiAxCiAgICB9LAogICAgewogICAgICAiYWRkciI6ICJqdW5vMXNsNXVkeG1uZGg3eDk5djJwMzJsdDM0amNoanlleG03NnQ0OTdtIiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xd3QyOWU3ZWM1ZjA0eHk2ZXo1bTZhZ3pyd2VoMHZ4c3UzdWNjNTUiLAogICAgICAid2VpZ2h0IjogMQogICAgfSwKICAgIHsKICAgICAgImFkZHIiOiAianVubzFlY2syN3FlZnR0dDV0d3hzZzM4Z3NyMHEwaHI0ZTN2dnl4bTJxNCIsCiAgICAgICJ3ZWlnaHQiOiAxCiAgICB9CiAgXQp9
```

## Complete SubDAO instantiation message

Here is the complete SubDAO instantiation message for the Juno Growth Fund. Note, the admin is set to the [Juno Community Pool](https://www.mintscan.io/juno/account/juno1jv65s3grqf6v6jl3dp4t6c9t9rk99cd83d88wr), meaning Juno Governance has complete power over this SubDAO.

```json
{
  "admin": "juno1jv65s3grqf6v6jl3dp4t6c9t9rk99cd83d88wr",
  "automatically_add_cw20s": false,
  "automatically_add_cw721s": false,
  "description": "The Delagations SubDAO is an official SubDAO of Juno Network, responsible for defining and managing the Juno Delegation Program.",
  "image_url": "https://cloudflare-ipfs.com/ipfs/QmVepcbAPgcS3q3n58xFvqo4zfvrPMm6KBhZYk3iVqLN2F",
  "name": "Juno Delegations SubDAO",
  "proposal_modules_instantiate_info": [
    {
      "admin": {
        "core_contract": {}
      },
      "code_id": 427,
      "label": "Delagations SubDAO proposal-single",
      "msg": "eyJhbGxvd19yZXZvdGluZyI6dHJ1ZSwibWF4X3ZvdGluZ19wZXJpb2QiOnsidGltZSI6NjA0ODAwfSwib25seV9tZW1iZXJzX2V4ZWN1dGUiOnRydWUsInRocmVzaG9sZCI6eyJhYnNvbHV0ZV9jb3VudCI6eyJ0aHJlc2hvbGQiOiI1In19fQ=="
    }
  ],
  "voting_module_instantiate_info": {
    "admin": {
      "core_contract": {}
    },
    "code_id": 429,
    "label": "Delagations SubDAO cw4-voting",
    "msg": "ewogICJjdzRfZ3JvdXBfY29kZV9pZCI6IDQzNCwKICAiaW5pdGlhbF9tZW1iZXJzIjogWwogICAgewogICAgICAiYWRkciI6ICJqdW5vMXMzM3pjdDJ6aGhhZjYweDRhOTBjcGU5eXF1dzk5amowemVuOHB0IiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xOHF3OXlkcGV3aDQwNXc0bHZtdWhsZzlndGFlcDc5dnkyZ210cjIiLAogICAgICAid2VpZ2h0IjogMQogICAgfSwKICAgIHsKICAgICAgImFkZHIiOiAianVubzE5bXhwNXllOGVzM241cDA4eGt4ZzJxbDkwYThmdzZqZXVmbXVmNiIsCiAgICAgICJ3ZWlnaHQiOiAxCiAgICB9LAogICAgewogICAgICAiYWRkciI6ICJqdW5vMThyN3VkOXBsaHh4OTBzaHN6MmNuYWhocWZzZm1oY3VoYXhzdXF6IiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xem5zbjBxZnZqc3RjYWh2bHY2MnM2OXh4OWxydDdzZmRycWV3eXAiLAogICAgICAid2VpZ2h0IjogMQogICAgfSwKICAgIHsKICAgICAgImFkZHIiOiAianVubzF1c3M4bHVmYTk3cG1kN2V6bHN2dG5xY21td3F3eGtkMHd0aGdmZyIsCiAgICAgICJ3ZWlnaHQiOiAxCiAgICB9LAogICAgewogICAgICAiYWRkciI6ICJqdW5vMXNsNXVkeG1uZGg3eDk5djJwMzJsdDM0amNoanlleG03NnQ0OTdtIiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xd3QyOWU3ZWM1ZjA0eHk2ZXo1bTZhZ3pyd2VoMHZ4c3UzdWNjNTUiLAogICAgICAid2VpZ2h0IjogMQogICAgfSwKICAgIHsKICAgICAgImFkZHIiOiAianVubzFlY2syN3FlZnR0dDV0d3hzZzM4Z3NyMHEwaHI0ZTN2dnl4bTJxNCIsCiAgICAgICJ3ZWlnaHQiOiAxCiAgICB9CiAgXQp9"
  }
}
```

## Full command used to create the proposal

The full command used to create the proposal specifies the code id, the CosmWasm smart contract code to use for contract instantiation. 432 corresponds to the DAO DAO core module.

It also sets the community pool as admin over all instantiated smart contracts, giving it the ability upgrade or migrate contracts if need be.

```bash
junod tx gov submit-proposal instantiate-contract 432 '{
  "admin": "juno1jv65s3grqf6v6jl3dp4t6c9t9rk99cd83d88wr",
  "automatically_add_cw20s": false,
  "automatically_add_cw721s": false,
  "description": "The Delagations SubDAO is an official SubDAO of Juno Network, responsible for defining and managing the Juno Delegation Program.",
  "image_url": "https://cloudflare-ipfs.com/ipfs/QmVepcbAPgcS3q3n58xFvqo4zfvrPMm6KBhZYk3iVqLN2F",
  "name": "Juno Delegations SubDAO",
  "proposal_modules_instantiate_info": [
    {
      "admin": {
        "core_contract": {}
      },
      "code_id": 427,
      "label": "Delagations SubDAO proposal-single",
      "msg": "eyJhbGxvd19yZXZvdGluZyI6dHJ1ZSwibWF4X3ZvdGluZ19wZXJpb2QiOnsidGltZSI6NjA0ODAwfSwib25seV9tZW1iZXJzX2V4ZWN1dGUiOnRydWUsInRocmVzaG9sZCI6eyJhYnNvbHV0ZV9jb3VudCI6eyJ0aHJlc2hvbGQiOiI1In19fQ=="
    }
  ],
  "voting_module_instantiate_info": {
    "admin": {
      "core_contract": {}
    },
    "code_id": 429,
    "label": "Delagations SubDAO cw4-voting",
    "msg": "ewogICJjdzRfZ3JvdXBfY29kZV9pZCI6IDQzNCwKICAiaW5pdGlhbF9tZW1iZXJzIjogWwogICAgewogICAgICAiYWRkciI6ICJqdW5vMXMzM3pjdDJ6aGhhZjYweDRhOTBjcGU5eXF1dzk5amowemVuOHB0IiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xOHF3OXlkcGV3aDQwNXc0bHZtdWhsZzlndGFlcDc5dnkyZ210cjIiLAogICAgICAid2VpZ2h0IjogMQogICAgfSwKICAgIHsKICAgICAgImFkZHIiOiAianVubzE5bXhwNXllOGVzM241cDA4eGt4ZzJxbDkwYThmdzZqZXVmbXVmNiIsCiAgICAgICJ3ZWlnaHQiOiAxCiAgICB9LAogICAgewogICAgICAiYWRkciI6ICJqdW5vMThyN3VkOXBsaHh4OTBzaHN6MmNuYWhocWZzZm1oY3VoYXhzdXF6IiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xem5zbjBxZnZqc3RjYWh2bHY2MnM2OXh4OWxydDdzZmRycWV3eXAiLAogICAgICAid2VpZ2h0IjogMQogICAgfSwKICAgIHsKICAgICAgImFkZHIiOiAianVubzF1c3M4bHVmYTk3cG1kN2V6bHN2dG5xY21td3F3eGtkMHd0aGdmZyIsCiAgICAgICJ3ZWlnaHQiOiAxCiAgICB9LAogICAgewogICAgICAiYWRkciI6ICJqdW5vMXNsNXVkeG1uZGg3eDk5djJwMzJsdDM0amNoanlleG03NnQ0OTdtIiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xd3QyOWU3ZWM1ZjA0eHk2ZXo1bTZhZ3pyd2VoMHZ4c3UzdWNjNTUiLAogICAgICAid2VpZ2h0IjogMQogICAgfSwKICAgIHsKICAgICAgImFkZHIiOiAianVubzFlY2syN3FlZnR0dDV0d3hzZzM4Z3NyMHEwaHI0ZTN2dnl4bTJxNCIsCiAgICAgICJ3ZWlnaHQiOiAxCiAgICB9CiAgXQp9"
  }
}' --label "Delegations SubDAO" --title "Launch Delegations SubDAO" --description "Juno **Delegation SubDAO** will be in charge of delegations for the Core Developer Fund, including all required collation of information, scoring of validator contributions, delegating tokens to validators on behalf of the Developer Fund wallet, and maintaining and updating the delegation criteria.\n\nThe SubDAO will be granted delegation rights through the AuthZ module and will execute delegations through a DAODAO multisig.\n\nThe SubDAO will collate all available information and score contributions every quarter.\n\nMembers:\n\n-   [Rarma_ (Community Member)](https://twitter.com/Rarma_)\n-   [MaxJuno (Wombat / Juno Core Contributer)](https://twitter.com/max_maxsolo)\n-   [Thyborg (Community Member)](https://twitter.com/Thyborg_)\n-   [Joshua Tan (Metagov)](https://twitter.com/joshuaztan)\n-   [Nullmames (Kingnodes / Juno Core Contributor)](https://twitter.com/nullMames)\n-   [Dimi (Core Root)](https://twitter.com/dimiandre)\n-   [Jake (Core Root / DAODAO)](https://twitter.com/JakeHartnell)\n-   [Daniel Hwang (Community Member / Governance Specialist)](https://twitter.com/danhwang88)\n-   [Community Staking (CommunityStaking Validator)](https://twitter.com/CommunityStakin)\n\nMembers of the community can apply to be part of the SubDao anytime in our forum. In the first committee round we'd like to include also Dimi and Jake to help smooth out the transition of the delegation program from Core 1 to the SubDao.\n\nIn accordance with [Prop 25](https://www.mintscan.io/juno/proposals/25) the SubDAO Multisig contract will be instantiated by this governance vote with the Juno community as admin. This means the community can execute messages on behalf of the DAO via a governance proposal, recall funds, upgrade the contract, or add / remove members.\n\nNote, the address of the Juno governance module and community pool is [juno1jv65s3grqf6v6jl3dp4t6c9t9rk99cd83d88wr](https://www.mintscan.io/juno/account/juno1jv65s3grqf6v6jl3dp4t6c9t9rk99cd83d88wr)\n\n### Verifying the SubDAO Instantiation Message\nInformation on verifying and understanding the SubDAO Instantiation message and how it works can be found [here](https://gist.github.com/JakeHartnell/43dc75abc91015b9d09bfe25d7899dac).\n\n=========\n\nBy voting **YES**, you agree the Juno Delegation SubDAO should be created as stated in this proposal.\n\nBy voting **NO** it means you do not want the Juno Delegation SubDAO to be created.\n\nBy voting **ABSTAIN**, you formally decline to vote either for or against the proposal.\n\nVoting **NOWITHVETO** expresses that you would like to see depositors penalized by revocation of their 500 JUNO deposit, and contributes towards an automatic 1/3 veto threshold.\n" --run-as juno1jv65s3grqf6v6jl3dp4t6c9t9rk99cd83d88wr --admin juno1jv65s3grqf6v6jl3dp4t6c9t9rk99cd83d88wr --amount 0ujuno --from <your-key> --gas-prices 0.025ujuno --gas 3000000
```

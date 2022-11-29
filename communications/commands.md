# Communications SubDAO Creation Proposal

This gist breaks down and explains the Communications SubDAO instantiation message.

For context, the instantiation message creates a new smart contract. In DAO DAO, the instantiation message actually creates multiple smart contracts that constitute the DAO.


## Proposal module instantiate message

The proposal module contains the settings for voting and execution of proposals.

Revoting is allowed, meaning members can change their votes up until the proposal has passed if they have recieved new information. For a proposal to pass, 5 / 8 members must vote YES. The voting period is 7 days.

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
      "addr": "juno1camelv4qedpzspggyu659cla4t6657rehy3lx3",
      "weight": 1
    },
    {
      "addr": "juno17py8gfneaam64vt9kaec0fseqwxvkq0flmsmhg",
      "weight": 1
    },
    {
      "addr": "juno125p5e2vzfcrm6xwmeuwk6qysun6jhh4x52kwkf",
      "weight": 1
    },
    {
      "addr": "juno19mxp5ye8es3n5p08xkxg2ql90a8fw6jeufmuf6",
      "weight": 1
    },
    {
      "addr": "juno1xssgajghl2hapljcgff5qplqnnn6f25ddjrhc9",
      "weight": 1
    },
    {
      "addr": "juno1xl8ch7ls4p3eyygt2pthuz6ek6sta2m07q5w4t",
      "weight": 1
    },
    {
      "addr": "juno1twh6302lzcvn7lr3x0fjwfkgryn9ac5c0xs5rs",
      "weight": 1
    }
  ]
}
```

Encoded as base64 (which you can verify using a base64 decoder like [this one](https://www.base64decode.org/)):

```
ewogICJjdzRfZ3JvdXBfY29kZV9pZCI6IDQzNCwKICAiaW5pdGlhbF9tZW1iZXJzIjogWwogICAgewogICAgICAiYWRkciI6ICJqdW5vMXMzM3pjdDJ6aGhhZjYweDRhOTBjcGU5eXF1dzk5amowemVuOHB0IiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xY2FtZWx2NHFlZHB6c3BnZ3l1NjU5Y2xhNHQ2NjU3cmVoeTNseDMiLAogICAgICAid2VpZ2h0IjogMQogICAgfSwKICAgIHsKICAgICAgImFkZHIiOiAianVubzE3cHk4Z2ZuZWFhbTY0dnQ5a2FlYzBmc2Vxd3h2a3EwZmxtc21oZyIsCiAgICAgICJ3ZWlnaHQiOiAxCiAgICB9LAogICAgewogICAgICAiYWRkciI6ICJqdW5vMTI1cDVlMnZ6ZmNybTZ4d21ldXdrNnF5c3VuNmpoaDR4NTJrd2tmIiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xOW14cDV5ZThlczNuNXAwOHhreGcycWw5MGE4Znc2amV1Zm11ZjYiLAogICAgICAid2VpZ2h0IjogMQogICAgfSwKICAgIHsKICAgICAgImFkZHIiOiAianVubzF4c3NnYWpnaGwyaGFwbGpjZ2ZmNXFwbHFubm42ZjI1ZGRqcmhjOSIsCiAgICAgICJ3ZWlnaHQiOiAxCiAgICB9LAogICAgewogICAgICAiYWRkciI6ICJqdW5vMXhsOGNoN2xzNHAzZXl5Z3QycHRodXo2ZWs2c3RhMm0wN3E1dzR0IiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xdHdoNjMwMmx6Y3ZuN2xyM3gwZmp3ZmtncnluOWFjNWMweHM1cnMiLAogICAgICAid2VpZ2h0IjogMQogICAgfQogIF0KfQ==
```

## Complete SubDAO instantiation message

Here is the complete SubDAO instantiation message for the Juno Growth Fund. Note, the admin is set to the [Juno Community Pool](https://www.mintscan.io/juno/account/juno1jv65s3grqf6v6jl3dp4t6c9t9rk99cd83d88wr), meaning Juno Governance has complete power over this SubDAO.

```json
{
  "admin": "juno1jv65s3grqf6v6jl3dp4t6c9t9rk99cd83d88wr",
  "automatically_add_cw20s": false,
  "automatically_add_cw721s": false,
  "description": "The Communications SubDAO is an official SubDAO of Juno Network, responsible for handling the image and branding of Juno in the outside world.",
  "image_url": "https://cloudflare-ipfs.com/ipfs/QmRyFwRozSVFAedQ6F3kCfmkc9AJTYBocGovY2zJHPi8n9",
  "name": "Juno Communications SubDAO",
  "proposal_modules_instantiate_info": [
    {
      "admin": {
        "core_contract": {}
      },
      "code_id": 427,
      "label": "Communications SubDAO proposal-single",
      "msg": "eyJhbGxvd19yZXZvdGluZyI6dHJ1ZSwibWF4X3ZvdGluZ19wZXJpb2QiOnsidGltZSI6NjA0ODAwfSwib25seV9tZW1iZXJzX2V4ZWN1dGUiOnRydWUsInRocmVzaG9sZCI6eyJhYnNvbHV0ZV9jb3VudCI6eyJ0aHJlc2hvbGQiOiI1In19fQ=="
    }
  ],
  "voting_module_instantiate_info": {
    "admin": {
      "core_contract": {}
    },
    "code_id": 429,
    "label": "Communications SubDAO cw4-voting",
    "msg": "ewogICJjdzRfZ3JvdXBfY29kZV9pZCI6IDQzNCwKICAiaW5pdGlhbF9tZW1iZXJzIjogWwogICAgewogICAgICAiYWRkciI6ICJqdW5vMXMzM3pjdDJ6aGhhZjYweDRhOTBjcGU5eXF1dzk5amowemVuOHB0IiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xY2FtZWx2NHFlZHB6c3BnZ3l1NjU5Y2xhNHQ2NjU3cmVoeTNseDMiLAogICAgICAid2VpZ2h0IjogMQogICAgfSwKICAgIHsKICAgICAgImFkZHIiOiAianVubzE3cHk4Z2ZuZWFhbTY0dnQ5a2FlYzBmc2Vxd3h2a3EwZmxtc21oZyIsCiAgICAgICJ3ZWlnaHQiOiAxCiAgICB9LAogICAgewogICAgICAiYWRkciI6ICJqdW5vMTI1cDVlMnZ6ZmNybTZ4d21ldXdrNnF5c3VuNmpoaDR4NTJrd2tmIiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xOW14cDV5ZThlczNuNXAwOHhreGcycWw5MGE4Znc2amV1Zm11ZjYiLAogICAgICAid2VpZ2h0IjogMQogICAgfSwKICAgIHsKICAgICAgImFkZHIiOiAianVubzF4c3NnYWpnaGwyaGFwbGpjZ2ZmNXFwbHFubm42ZjI1ZGRqcmhjOSIsCiAgICAgICJ3ZWlnaHQiOiAxCiAgICB9LAogICAgewogICAgICAiYWRkciI6ICJqdW5vMXhsOGNoN2xzNHAzZXl5Z3QycHRodXo2ZWs2c3RhMm0wN3E1dzR0IiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xdHdoNjMwMmx6Y3ZuN2xyM3gwZmp3ZmtncnluOWFjNWMweHM1cnMiLAogICAgICAid2VpZ2h0IjogMQogICAgfQogIF0KfQ=="
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
  "description": "The Communications SubDAO is an official SubDAO of Juno Network, responsible for handling the image and branding of Juno in the outside world.",
  "image_url": "https://cloudflare-ipfs.com/ipfs/QmRyFwRozSVFAedQ6F3kCfmkc9AJTYBocGovY2zJHPi8n9",
  "name": "Juno Communications SubDAO",
  "proposal_modules_instantiate_info": [
    {
      "admin": {
        "core_contract": {}
      },
      "code_id": 427,
      "label": "Communications SubDAO proposal-single",
      "msg": "eyJhbGxvd19yZXZvdGluZyI6dHJ1ZSwibWF4X3ZvdGluZ19wZXJpb2QiOnsidGltZSI6NjA0ODAwfSwib25seV9tZW1iZXJzX2V4ZWN1dGUiOnRydWUsInRocmVzaG9sZCI6eyJhYnNvbHV0ZV9jb3VudCI6eyJ0aHJlc2hvbGQiOiI1In19fQ=="
    }
  ],
  "voting_module_instantiate_info": {
    "admin": {
      "core_contract": {}
    },
    "code_id": 429,
    "label": "Communications SubDAO cw4-voting",
    "msg": "ewogICJjdzRfZ3JvdXBfY29kZV9pZCI6IDQzNCwKICAiaW5pdGlhbF9tZW1iZXJzIjogWwogICAgewogICAgICAiYWRkciI6ICJqdW5vMXMzM3pjdDJ6aGhhZjYweDRhOTBjcGU5eXF1dzk5amowemVuOHB0IiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xY2FtZWx2NHFlZHB6c3BnZ3l1NjU5Y2xhNHQ2NjU3cmVoeTNseDMiLAogICAgICAid2VpZ2h0IjogMQogICAgfSwKICAgIHsKICAgICAgImFkZHIiOiAianVubzE3cHk4Z2ZuZWFhbTY0dnQ5a2FlYzBmc2Vxd3h2a3EwZmxtc21oZyIsCiAgICAgICJ3ZWlnaHQiOiAxCiAgICB9LAogICAgewogICAgICAiYWRkciI6ICJqdW5vMTI1cDVlMnZ6ZmNybTZ4d21ldXdrNnF5c3VuNmpoaDR4NTJrd2tmIiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xOW14cDV5ZThlczNuNXAwOHhreGcycWw5MGE4Znc2amV1Zm11ZjYiLAogICAgICAid2VpZ2h0IjogMQogICAgfSwKICAgIHsKICAgICAgImFkZHIiOiAianVubzF4c3NnYWpnaGwyaGFwbGpjZ2ZmNXFwbHFubm42ZjI1ZGRqcmhjOSIsCiAgICAgICJ3ZWlnaHQiOiAxCiAgICB9LAogICAgewogICAgICAiYWRkciI6ICJqdW5vMXhsOGNoN2xzNHAzZXl5Z3QycHRodXo2ZWs2c3RhMm0wN3E1dzR0IiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xdHdoNjMwMmx6Y3ZuN2xyM3gwZmp3ZmtncnluOWFjNWMweHM1cnMiLAogICAgICAid2VpZ2h0IjogMQogICAgfQogIF0KfQ=="
  }
}' --label "Communications SubDAO" --title "Launch Communications SubDAO" --description "**Juno Communications SubDAO** is a group of individuals with the responsibility of handling the image and branding of Juno in the outside world. They are also in charge of organizing conferences or providing funds for it, creating online campaigns, strategic partnerships and community events. It is responsible for making Juno Network and its dApps & builders well known.\n\n_Commonwealth discussion_: https://commonwealth.im/juno/discussion/7475-launch-communications-subdao\n\n## Objectives\n\n- Keeping the community updated by sharing news of what is currently going on and being built out on Juno Network as well as future developments.\n\n- Attract new community members through hosting campaigns and events around the world.\n\n- Manage and promote the Juno brand across both traditional and Web3 world.\n\n- Create merchandise and swag for conferences and online shopping, independently or through partners.\n\n- Give support and recognition to Juno partners and projects building on the network, both through social media and traditional press releases and news channels. Helping to spread the Cosmos Interchain Ecosystem vision and Juno’s unique place within it.\n\n- Educate both new and current users & developers about projects and tooling built on both Juno and the interchain.\n\n- Helping to promote and showcase Juno’s bleeding-edge features and integrations with CosmWasm to users and developers.\n\n- Support the various Cosmos events and Hackathons, to mention some: Cosmoverse, HackAtom, HackWasm.\n\n- Introducing Juno & CosmWasm to various non-Cosmos events and Hackathons outside the Cosmos ecosystem, to mention some: (Eth conferences go here)\n\n- Administrate Telegram, Discord and other chats to keep the public updated with news and information.\n\n- Overseeing the creation of both written articles and videos which showcase the dApps being built on Juno, and the features and capabilities Juno provides to users and developers.\n\n- Coordinating with other official SubDAOs on newsworthy developments and events and promoting them in press releases and social media.\n\n- Create graphic designs i.e banners, flyers, etc for events or social media.\n\nThe SubDAO will also have direct or indirect full access to Juno Social Media channels, website repositories and will also have the possibility to cooperate with a future Infrastructure DAO (not existing yet) to manage domain DNS and emails.\n\n## Members\n\n**Initial members**\n\n- Highlander (Public & Partners communications)\n\n- MaxJuno (Community Management)\n\n- CamelJuno (Web Dev, UI/UX/GFX Design)\n\n- Traiano (Space Merch, Made in Block) \n\n- Lukas (Videos)\n\n- CryptoCakir (Ambassador Program)\n\n**Temporary members for bootstrap**\n\n- Block Creators (Core Root)\n\n- Dimi (Core Root)\n\n**Open Spots**\n\n- (Open spot) Director of the SubDAO\n\n- (Open spot) Social media manager\n\n- (Open spot) Twitter spaces, content creator\n\n- (Open spot) Copywriter\n\nAnyone can apply to be part of the Communications SubDAO using the appropriate section on commonwealth.\n\n## Funding\n\nThe SubDAO will be initially funded with around 20,000~ JUNO from the previous marketing multi-sig, and will ask for additional funding from the community pool when needed.\n\nFunds will be spent on the following:\n\n- Pay salaries of full-time and part-time people working on this\n\n- Pay eventual outsourcing work or external partners\n\n- Allocate to community-incentivized events\n\n- All of the activities described under “Objectives” above.\n\nCore Root members or people with salary from other SubDAOs or other Juno Entities will not get a double salary from this and will participate only for decision-making or as guarantee to the SubDAO good faith.\n\nQuarterly reports will be shared with the community as a recap of operations and results.\n\n## Deployment\n\nIn accordance with [Prop 25](https://www.mintscan.io/juno/proposals/25), the SubDAO Multisig contract will be instantiated by this governance vote with the Juno community DAO as admin. This means the community can execute messages on behalf of the subDAO via a governance proposal, recall funds back to the community pool, upgrade the contract, or add / remove members.\n\nThe Communications subDAO will operate while abiding by the principles defined in [Prop 25](https://www.mintscan.io/juno/proposals/25).\n\nNote, the address of the Juno governance module and community pool is [juno1jv65s3grqf6v6jl3dp4t6c9t9rk99cd83d88wr](https://www.mintscan.io/juno/account/juno1jv65s3grqf6v6jl3dp4t6c9t9rk99cd83d88wr).\n\nJuno community will have full visibility of the subDAO spending using DAODAO interface.\n\nNo community pool funds are requested at this stage.\n\n=========\n\nBy voting **YES**, you agree the Juno Communications SubDAO should be created as stated in this proposal.\n\nBy voting **NO** it means you disagree that the Juno Communications SubDAO should be created.\n\nBy voting **ABSTAIN**, you formally decline to vote either for or against the proposal.\n\nVoting **NOWITHVETO** expresses that you disagree with the proposition and additionally want to see depositors penalized by revocation of their 1000 JUNO deposit, which contributes towards an automatic 1/3 veto threshold" --run-as juno1jv65s3grqf6v6jl3dp4t6c9t9rk99cd83d88wr --admin juno1jv65s3grqf6v6jl3dp4t6c9t9rk99cd83d88wr --amount 0ujuno --from <your-key> --gas-prices 0.025ujuno --gas 10000000
```

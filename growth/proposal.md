# Grow Juno SubDAO Creation Proposal

This gist breaks down and explains the Juno Growth Fund SubDAO instantiation message.

For context, the CosmWasm instantiation message creates a new smart contract. In [DAO DAO](https://daodao.zone), the instantiation message actually creates multiple smart contracts that constitute the DAO.

## Proposal module instantiate message

The proposal module contains the settings for voting and execution of proposals.

Revoting is allowed, meaning members can change their votes up until the proposal has passed if they have recieved new information. For a proposal to pass, 6 / 11 members must vote YES. The voting period is 5 days.

Only members of the SubDAO can execute a proposal once it is passed.

```json
{"allow_revoting":true,"max_voting_period":{"time":432000},"only_members_execute":true,"threshold":{"absolute_count":{"threshold":"6"}}}
```

Encoded as base64 (which you can verify using a base64 decoder like [this one](https://www.base64decode.org/)):

```
eyJhbGxvd19yZXZvdGluZyI6dHJ1ZSwibWF4X3ZvdGluZ19wZXJpb2QiOnsidGltZSI6NDMyMDAwfSwib25seV9tZW1iZXJzX2V4ZWN1dGUiOnRydWUsInRocmVzaG9sZCI6eyJhYnNvbHV0ZV9jb3VudCI6eyJ0aHJlc2hvbGQiOiI2In19fQ==
```

## Voting module instantiate message

The voting module determins who has voting power in the DAO. In this case, this list is managed by a `cw4-groups` contract. Each member of the Juno Growth Fund SubDAO has submitted their addresses, and will each have a voting power of 1.

```json
{
  "cw4_group_code_id": 434,
  "initial_members": [
    {
      "addr": "juno1jwxjzpwdtglf7a35sackv0dn0hr9nk6h6ctsh4",
      "weight": 1
    },
    {
      "addr": "juno1eck27qefttt5twxsg38gsr0q0hr4e3vvyxm2q4",
      "weight": 1
    },
    {
      "addr": "juno1njyvry0t3j5dy4rr6ar5zfglg3cy2e8u745hl7",
      "weight": 1
    },
    {
      "addr": "juno1e6fhmfer34hh7kl9um6p52nkqflkp4jajgxunw",
      "weight": 1
    },
    {
      "addr": "juno1phcqn3pzpwv34qg754nhswjrztwrlfaxyhxgku",
      "weight": 1
    },
    {
      "addr": "juno1ctrx5p95ypr04n7ksxenjug79zkjkz4sjft8gl",
      "weight": 1
    },
    {
      "addr": "juno1dvpyr5j5hsdtdw33kpf8xgypu7jnpf02udjyy7",
      "weight": 1
    },
    {
      "addr": "juno12ls39vndhd55c5dm7ufund4kvzg6hrw50r0tdz",
      "weight": 1
    },
    {
      "addr": "juno1ghe0uuat7zrj9qqw2pznwutdgr9u05kfs52rkd",
      "weight": 1
    },
    {
      "addr": "juno1q4ar2jwef0zdwmr4xwesxdgxnnkwfvl2m9p2e4",
      "weight": 1
    },
    {
      "addr": "juno1ha02l778d999dfk09d9d7gvd69g0hn7zxnkg8u",
      "weight": 1
    }
  ]
}
```

Encoded as base64 (which you can verify using a base64 decoder like [this one](https://www.base64decode.org/)):

```
ewogICJjdzRfZ3JvdXBfY29kZV9pZCI6IDQzNCwKICAiaW5pdGlhbF9tZW1iZXJzIjogWwogICAgewogICAgICAiYWRkciI6ICJqdW5vMWp3eGp6cHdkdGdsZjdhMzVzYWNrdjBkbjBocjluazZoNmN0c2g0IiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xZWNrMjdxZWZ0dHQ1dHd4c2czOGdzcjBxMGhyNGUzdnZ5eG0ycTQiLAogICAgICAid2VpZ2h0IjogMQogICAgfSwKICAgIHsKICAgICAgImFkZHIiOiAianVubzFuanl2cnkwdDNqNWR5NHJyNmFyNXpmZ2xnM2N5MmU4dTc0NWhsNyIsCiAgICAgICJ3ZWlnaHQiOiAxCiAgICB9LAogICAgewogICAgICAiYWRkciI6ICJqdW5vMWU2ZmhtZmVyMzRoaDdrbDl1bTZwNTJua3FmbGtwNGphamd4dW53IiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xcGhjcW4zcHpwd3YzNHFnNzU0bmhzd2pyenR3cmxmYXh5aHhna3UiLAogICAgICAid2VpZ2h0IjogMQogICAgfSwKICAgIHsKICAgICAgImFkZHIiOiAianVubzFjdHJ4NXA5NXlwcjA0bjdrc3hlbmp1Zzc5emtqa3o0c2pmdDhnbCIsCiAgICAgICJ3ZWlnaHQiOiAxCiAgICB9LAogICAgewogICAgICAiYWRkciI6ICJqdW5vMWR2cHlyNWo1aHNkdGR3MzNrcGY4eGd5cHU3am5wZjAydWRqeXk3IiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xMmxzMzl2bmRoZDU1YzVkbTd1ZnVuZDRrdnpnNmhydzUwcjB0ZHoiLAogICAgICAid2VpZ2h0IjogMQogICAgfSwKICAgIHsKICAgICAgImFkZHIiOiAianVubzFnaGUwdXVhdDd6cmo5cXF3MnB6bnd1dGRncjl1MDVrZnM1MnJrZCIsCiAgICAgICJ3ZWlnaHQiOiAxCiAgICB9LAogICAgewogICAgICAiYWRkciI6ICJqdW5vMXE0YXIyandlZjB6ZHdtcjR4d2VzeGRneG5ua3dmdmwybTlwMmU0IiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xaGEwMmw3NzhkOTk5ZGZrMDlkOWQ3Z3ZkNjlnMGhuN3p4bmtnOHUiLAogICAgICAid2VpZ2h0IjogMQogICAgfQogIF0KfQo=
```

## Complete SubDAO instantiation message

Here is the complete SubDAO instantiation message for the Juno Growth Fund. Note, the admin is set to the [Juno Community Pool](https://www.mintscan.io/juno/account/juno1jv65s3grqf6v6jl3dp4t6c9t9rk99cd83d88wr), meaning Juno Governance has complete power over this SubDAO.

```json
{
  "admin": "juno1jv65s3grqf6v6jl3dp4t6c9t9rk99cd83d88wr",
  "automatically_add_cw20s": false,
  "automatically_add_cw721s": false,
  "description": "The Juno Growth Fund is an official SubDAO of Juno Network, responsible for the long-term growth and sustainability of the network, and seeks to enable builders which will accrue substantial value to the network and its stakers.",
  "image_url": "https://cloudflare-ipfs.com/ipfs/bafkreigznjnnoy3cad5it6kldii2zsmxhtq7pa3caigbhka36x7gbbzjde",
  "name": "Juno Growth Fund",
  "proposal_modules_instantiate_info": [
    {
      "admin": {
        "core_contract": {}
      },
      "code_id": 427,
      "label": "JGF proposal-single",
      "msg": "eyJhbGxvd19yZXZvdGluZyI6dHJ1ZSwibWF4X3ZvdGluZ19wZXJpb2QiOnsidGltZSI6NDMyMDAwfSwib25seV9tZW1iZXJzX2V4ZWN1dGUiOnRydWUsInRocmVzaG9sZCI6eyJhYnNvbHV0ZV9jb3VudCI6eyJ0aHJlc2hvbGQiOiI2In19fQ=="
    }
  ],
  "voting_module_instantiate_info": {
    "admin": {
      "core_contract": {}
    },
    "code_id": 429,
    "label": "JGF cw4-voting",
    "msg": "ewogICJjdzRfZ3JvdXBfY29kZV9pZCI6IDQzNCwKICAiaW5pdGlhbF9tZW1iZXJzIjogWwogICAgewogICAgICAiYWRkciI6ICJqdW5vMWp3eGp6cHdkdGdsZjdhMzVzYWNrdjBkbjBocjluazZoNmN0c2g0IiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xZWNrMjdxZWZ0dHQ1dHd4c2czOGdzcjBxMGhyNGUzdnZ5eG0ycTQiLAogICAgICAid2VpZ2h0IjogMQogICAgfSwKICAgIHsKICAgICAgImFkZHIiOiAianVubzFuanl2cnkwdDNqNWR5NHJyNmFyNXpmZ2xnM2N5MmU4dTc0NWhsNyIsCiAgICAgICJ3ZWlnaHQiOiAxCiAgICB9LAogICAgewogICAgICAiYWRkciI6ICJqdW5vMWU2ZmhtZmVyMzRoaDdrbDl1bTZwNTJua3FmbGtwNGphamd4dW53IiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xcGhjcW4zcHpwd3YzNHFnNzU0bmhzd2pyenR3cmxmYXh5aHhna3UiLAogICAgICAid2VpZ2h0IjogMQogICAgfSwKICAgIHsKICAgICAgImFkZHIiOiAianVubzFjdHJ4NXA5NXlwcjA0bjdrc3hlbmp1Zzc5emtqa3o0c2pmdDhnbCIsCiAgICAgICJ3ZWlnaHQiOiAxCiAgICB9LAogICAgewogICAgICAiYWRkciI6ICJqdW5vMWR2cHlyNWo1aHNkdGR3MzNrcGY4eGd5cHU3am5wZjAydWRqeXk3IiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xMmxzMzl2bmRoZDU1YzVkbTd1ZnVuZDRrdnpnNmhydzUwcjB0ZHoiLAogICAgICAid2VpZ2h0IjogMQogICAgfSwKICAgIHsKICAgICAgImFkZHIiOiAianVubzFnaGUwdXVhdDd6cmo5cXF3MnB6bnd1dGRncjl1MDVrZnM1MnJrZCIsCiAgICAgICJ3ZWlnaHQiOiAxCiAgICB9LAogICAgewogICAgICAiYWRkciI6ICJqdW5vMXE0YXIyandlZjB6ZHdtcjR4d2VzeGRneG5ua3dmdmwybTlwMmU0IiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xaGEwMmw3NzhkOTk5ZGZrMDlkOWQ3Z3ZkNjlnMGhuN3p4bmtnOHUiLAogICAgICAid2VpZ2h0IjogMQogICAgfQogIF0KfQo="
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
  "description": "The Juno Growth Fund is an official SubDAO of Juno Network, responsible for the long-term growth and sustainability of the network, and seeks to enable builders which will accrue substantial value to the network and its stakers.",
  "image_url": "https://cloudflare-ipfs.com/ipfs/bafkreigznjnnoy3cad5it6kldii2zsmxhtq7pa3caigbhka36x7gbbzjde",
  "name": "Juno Growth Fund",
  "proposal_modules_instantiate_info": [
    {
      "admin": {
        "core_contract": {}
      },
      "code_id": 427,
      "label": "JGF proposal-single",
      "msg": "eyJhbGxvd19yZXZvdGluZyI6dHJ1ZSwibWF4X3ZvdGluZ19wZXJpb2QiOnsidGltZSI6NDMyMDAwfSwib25seV9tZW1iZXJzX2V4ZWN1dGUiOnRydWUsInRocmVzaG9sZCI6eyJhYnNvbHV0ZV9jb3VudCI6eyJ0aHJlc2hvbGQiOiI2In19fQ=="
    }
  ],
  "voting_module_instantiate_info": {
    "admin": {
      "core_contract": {}
    },
    "code_id": 429,
    "label": "JGF cw4-voting",
    "msg": "ewogICJjdzRfZ3JvdXBfY29kZV9pZCI6IDQzNCwKICAiaW5pdGlhbF9tZW1iZXJzIjogWwogICAgewogICAgICAiYWRkciI6ICJqdW5vMWp3eGp6cHdkdGdsZjdhMzVzYWNrdjBkbjBocjluazZoNmN0c2g0IiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xZWNrMjdxZWZ0dHQ1dHd4c2czOGdzcjBxMGhyNGUzdnZ5eG0ycTQiLAogICAgICAid2VpZ2h0IjogMQogICAgfSwKICAgIHsKICAgICAgImFkZHIiOiAianVubzFuanl2cnkwdDNqNWR5NHJyNmFyNXpmZ2xnM2N5MmU4dTc0NWhsNyIsCiAgICAgICJ3ZWlnaHQiOiAxCiAgICB9LAogICAgewogICAgICAiYWRkciI6ICJqdW5vMWU2ZmhtZmVyMzRoaDdrbDl1bTZwNTJua3FmbGtwNGphamd4dW53IiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xcGhjcW4zcHpwd3YzNHFnNzU0bmhzd2pyenR3cmxmYXh5aHhna3UiLAogICAgICAid2VpZ2h0IjogMQogICAgfSwKICAgIHsKICAgICAgImFkZHIiOiAianVubzFjdHJ4NXA5NXlwcjA0bjdrc3hlbmp1Zzc5emtqa3o0c2pmdDhnbCIsCiAgICAgICJ3ZWlnaHQiOiAxCiAgICB9LAogICAgewogICAgICAiYWRkciI6ICJqdW5vMWR2cHlyNWo1aHNkdGR3MzNrcGY4eGd5cHU3am5wZjAydWRqeXk3IiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xMmxzMzl2bmRoZDU1YzVkbTd1ZnVuZDRrdnpnNmhydzUwcjB0ZHoiLAogICAgICAid2VpZ2h0IjogMQogICAgfSwKICAgIHsKICAgICAgImFkZHIiOiAianVubzFnaGUwdXVhdDd6cmo5cXF3MnB6bnd1dGRncjl1MDVrZnM1MnJrZCIsCiAgICAgICJ3ZWlnaHQiOiAxCiAgICB9LAogICAgewogICAgICAiYWRkciI6ICJqdW5vMXE0YXIyandlZjB6ZHdtcjR4d2VzeGRneG5ua3dmdmwybTlwMmU0IiwKICAgICAgIndlaWdodCI6IDEKICAgIH0sCiAgICB7CiAgICAgICJhZGRyIjogImp1bm8xaGEwMmw3NzhkOTk5ZGZrMDlkOWQ3Z3ZkNjlnMGhuN3p4bmtnOHUiLAogICAgICAid2VpZ2h0IjogMQogICAgfQogIF0KfQo="
  }
}' --label "Juno Growth Fund SubDAO" --title "Creation of the Grow Juno SubDAO" --description '# Grow Juno SubDAO\n\nThe Juno community’s Terra Developer Fund has achieved its purpose. Since the passing of the Terra Developer Fund Proposal, 18 projects have pulled themselves from the wreckage of the Terra collapse and found a new home on Juno. In this process of delivering aid to Terra projects, we noticed that Terra developers aren’t the only ones who could use a little help. There are many new projects building on Juno, or who wish to build on Juno, that could benefit from community support.\n\nThe rapid ascent of projects on Juno has been fantastic, but in an increasingly competitive landscape, we must maintain this momentum and drive growth sustainably for the long term. We can now do this with the Growth Fund, one led by community members, operated transparently, and owned by Juno governance. We now have the time and opportunity to build up the ideal form of this DAO. We must have more human resources, diverse views, and representatives from the community - as well as a means to collaborate with outside capital partners to participate alongside the Juno Community in funding these protocols. The projects built in this bear market will define Juno’s future as a leader in the Cosmos, a home for projects and protocols, and a community-driven incubator for the CosmWasm interchain.\n\nThis proposal would transition the Terra Developer Fund into an official Grow Juno SubDAO. This proposal aims to expand the membership to include members from the community with professional investing experience, analyst skill sets and valuable business acumen. As a community initiative, we are purposefully aiming to have less representation from Core-1, and stronger representation from experts within the community.\n\nThis proposal will expand upon Proposal 23 by extending the scope beyond Terra migrations to include all new projects and investments conducive to the growth and development of Juno, to bring more value to Juno holders as a whole, as well as new investment opportunities which expand the Juno’s Community Pool and make it a sustainable resource for continued growth and community endeavors. \n\nThe [Terra Developer Fund Treasury](https://legacy.daodao.zone/multisig/juno1lgnstas4ruflg0eta394y8epq67s4rzhg5anssz3rc5zwvjmmvcql6qps2) will be transferred to the Grow Juno SubDAO and will seed the initial SubDAO treasury.\n\n## Creation of SubDAO\n\nIf passed, an official SubDAO will be created so that the Juno community maintains control of the SubDAO itself, and its associated treasury.\n\nAt the time of Prop 23 passing, the DAODAO SubDAO system was not available. Now that it is available, it is a much better setup than a normal multisig and with DAODAO V2 on the way, this will only make SubDAOs more effective.\n\n**Some key benefits are:**\n\n- Community control of SubDAO membership.\n- Community control of SubDAO treasury.\n- Formalization of the purpose of this SubDAO: To grow the overall ecosystem and bring in new capital.\n- Control from the community to return funds to the Community Pool, if it deems necessary.\n- Control from the community to add or remove members and the entire SubDAO, if it deems necessary.\n\n**Specific mandates:**\n\n1) The Grow Juno SubDAO will seek community approval (through on-chain signaling proposal) for any grants above $250k to any single entity.\n\n2) The Grow Juno SubDAO will actively seek out projects and investments which can contribute strong token swaps and/or obvious profits to the Community Pool, and will always aim to take actions which maintain the sustainability of the fund for the Juno community. In some cases, public goods may be funded, subject to the same limitations as above, insofar as they unlock key functionality for promising new protocols, (i.e. oracles, infrastructure partners, indexing, protocol code audits, etc)\n\n3) The Grow Juno SubDAO Treasury is subject to the control of the entire community. The community has the ability to cancel any outstanding funding and/or return funds to the community pool, at any time through governance, for any reason.\n\n4) The Grow Juno SubDAO membership will be established by governance, and will be maintained and changed using DAO voting, as necessary to accommodate and adjust its membership to the needs of the Juno Community. At any time, on-chain governance can override membership, as with all SubDAOs.\n\n5) As the membership is expanding, it’s important to mandate that, where notable conflicts of interest may occur, members are expected to vote to abstain and recuse themselves. Simply being an investor in a project shall not be deemed to be a conflict of interest.\n\n6) The Grow Juno SubDAO will encourage and assist protocols in seeking additional supplementary funding with outside capital and funding partners to lower the risk of funding issuance by the Juno community, and will help to bring in new capital to the ecosystem through venture partners.\n\n7) Being an investor in projects is encouraged, and many of the venture investors working alongside the DAO can and should take on the risk of investing in protocols coming into the ecosystem. This must be encouraged to spread risk/benefit amongst numerous entities, and not place the burden of protocol funding solely upon the Juno community. Investments shall be disclosed by members publicly.\n\n8) Members of the DAO should be paid modestly while proving their own continued effectiveness and the viability of the subDAO, but well enough to put in the hours required to achieve the goals of the subDAO. This will be implemented sustainably by staking a portion of the treasury so that funding is not depleted over time.\n\n9) These mandates can be changed only through SubDAO membership voting on DAODAO, in a manner fully visible to the Juno community.\n\n**The membership of this SubDAO is proposed to be as such:**\n\n6 of 11 required for funding approval\n\n- Kevin Garrison (Oni Validator + Juno Biz Dev)\n- Maxjuno (Community Outreach + DAO Coordination)\n- Pupmos (Technical Expertise, Validator)\n- GoldenRatioStaking (Contracts Negotiations, Real Estate Investor)\n- Rarma (Project Manager, Quality Assurance, Vetting)\n- Jonathan DeLine (Venture Experience, M&A, Advisor)\n- Wtrsld (NetaDAO + Venture Experience)\n- Avicenna - Kleomedes (Validator, Fund Experience, Yield Expert, Analytics)\n- BoringDAO Members (Cosmos Investment DAO: Rahul P., Jonathan K., Connor K., RJ Patel)\n- Jonathan Caras, (VC, Protocol Outreach, Project Specialist, Comms)\n- Matthew Cantieri (VC, Microsoft VC, Protocol Incubation)\n\n**Advisory Board to the subDAO:**\nThese are advisors to the subDAO, who have valuable insights and skills and will also serve as a pool of potential DAO members who can step in to take up a voting seat, when needed.\n\n- _BitN8 (Project Specialist, Vetting)_\n- _JaparJam (Web3 Builders Alliance, Developer Resources)_\n- _CamelJuno (Full Stack Dev, UI/UX/DX, C2 Contributor)_\n- _Soi2studios (Community + Investor)_\n- _Reece, Validator & Technical Expert - NotionalDAO_\n- _TendermintTimmy, (SparkIBC, Community Validator)_\n- _Joe Abbey (Community Validator, Technical Expert)_\n- _Highlander Nodes (Validator, C2 Contributor)_\n- _Gjermund Garaba (EmpowerChain, Dev, Validator)_\n- _CommunityStaking (Community Validator)_\n- _DelRey - Stakin (Community Validator)_\n\n### Verifying the SubDAO Instantiation Message\nInformation on verifying and understanding the SubDAO Instantiation message and how it works can be found [here](https://gist.github.com/JakeHartnell/95492da2508074e44b8e5cef01aebc5f).\n\n## Vote:\n\nBy voting **YES**, you agree the Grow Juno SubDAO should be created as per the above proposal.\n\nBy Voting **NO**, it means you do not believe the Juno Ecosystem Growth Fund should be created as per the above proposal.\n\nBy voting **ABSTAIN**, you formally decline to vote either for or against the proposal.\n\nVoting **NOWITHVETO** expresses that you would like to see depositors penalized by revocation of their proposal deposit, and contributes towards an automatic 1/3 veto threshold.\n' --run-as juno1jv65s3grqf6v6jl3dp4t6c9t9rk99cd83d88wr --admin juno1jv65s3grqf6v6jl3dp4t6c9t9rk99cd83d88wr --amount 0ujuno --from <keyname> --gas-prices 0.025ujuno --gas 3000000
```

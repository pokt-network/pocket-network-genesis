# Pocket Network Shannon Testnet

TODO(@olshansk, @okdas): This document is a work in progress and intended to keep
track of things we'll need in the genesis files along with supporting details.

- [Pocket Network Shannon Testnet](#pocket-network-shannon-testnet)
  - [Accounts](#accounts)
  - [Private keys](#private-keys)
  - [Ignite config.yaml](#ignite-configyaml)


## Accounts

- `pokt1f0c9y7mahf2ya8tymy8g4rr75ezh3pkklu4c3e` - DAO/PNF
- `pokt1fpxstscnqtzc9tq0u0nlvg69hqt6zhaxyka2mj` - faucet
- `pokt1kq2ecszhhrn0z3nwqgqkegeqhr9ftslu5t4ya5` - validator1
- `pokt15ux823wusfvvkw7y4nnqqx5s95ag5p8xwmj02z` - validator2
- `pokt17mgzg2wrq248yu5gpvp5adqgwl6s6xg47jdtm0` - validator3
- `pokt1a5f5hxgaxg83y6s5w8k47dpwylkms4jjjrl9l6` - validator4
- `pokt19csy3xzhpnzk8eu9ykjjzxk3vzma8gxz5rx3dy` - validator5

## Private keys

The TestNet is currently maintained by Grove. 

Information on how to get access to keys can be found [here](https://www.notion.so/buildwithgrove/Beta-TestNet-144a36edfff6802597a1fa4c39ef3fcb?pvs=4).

## Ignite config.yaml

The following ignite config was used:

```yaml
version: 1
build:
  main: cmd/poktrolld
accounts:
  - name: pnf
    address: pokt1f0c9y7mahf2ya8tymy8g4rr75ezh3pkklu4c3e
    coins:
      - 69420000000upokt
  - name: validator1
    coins:
      - 1000000001000000upokt
  - name: validator2
    coins:
      - 1000000001000000upokt
  - name: validator3
    coins:
      - 1000000001000000upokt
  - name: validator4
    coins:
      - 1000000001000000upokt
  - name: validator5
    coins:
      - 1000000001000000upokt
  - name: faucet
    coins:
      - 9999999999999999999999999999999999999999999999999999999999999999upokt
client:
  typescript:
    path: ts-client
  hooks:
    path: react/src/hooks
  openapi:
    path: docs/static/openapi.yml
validators:
  # Multi-validator support is ready but not released yet https://github.com/ignite/cli/issues/4374, https://github.com/ignite/cli/pull/4409#issue-2659096643
  - name: validator1
    bonded: 1000000000000000upokt
    app:
      telemetry:
        enabled: true
        prometheus-retention-time: "1800" # seconds
    config:
      moniker: "validator1"
      consensus:
        timeout_commit: "300s"
        timeout_propose: "300s"
      instrumentation:
        prometheus: true
      log_level: "info"
    client:
      chain-id: pocket-beta
    gentx:
      chain-id: pocket-beta

# We can persist arbitrary genesis values via 1 to 1 mapping to genesis.json
genesis:
  chain_id: pocket-beta
  app_state:
    # https://docs.cosmos.network/main/build/modules/mint
    mint:
      params:
        mint_denom: upokt
        # Note that in Pocket Network, the majority of the inflation/deflation
        # comes from the utility of network, not just the validators that
        # secure it. Therefore, the inflation params of x/mint are set to 0.
        # See x/tokenomics for all details related to token inflation.
        inflation_rate_change: "0.0"
        inflation_max: "0.0"
        inflation_min: "0.0"
        # These parameters are included for posterity but commented out for clarity
        # goal_bonded: "NA"
        # blocks_per_year: "NA"
        # max_supply: "NA"
    staking:
      params:
        bond_denom: upokt
        # TODO_BETA(@okdas): Update this to 10 for Beta TestNet.
        max_validators: 10
    crisis:
      constant_fee:
        amount: "10000"
        denom: upokt
    gov:
      params:
        min_deposit:
          - amount: "10000"
            denom: upokt
    application:
      params:
        max_delegated_gateways: "7"
        min_stake:
          # TODO_BETA(@bryanchriswhite): Determine realistic amount for minimum application stake amount.
          amount: "100000000" # 100 POKT
          denom: upokt
      applicationList: []
    supplier:
      params:
        # TODO_BETA(@bryanchriswhite): Determine realistic amount for minimum gateway stake amount.
        min_stake:
          amount: "1000000" # 1 POKT
          denom: upokt
      supplierList: []
    gateway:
      params:
        # TODO_BETA(@bryanchriswhite): Determine realistic amount for minimum gateway stake amount.
        min_stake:
          amount: "1000000" # 1 POKT
          denom: upokt
      gatewayList: []
    service:
      params:
        add_service_fee:
          amount: "1000000000"
          denom: upokt
      serviceList: []
    proof:
      params:
        proof_request_probability: "0.25"
        proof_requirement_threshold:
          amount: "20000000"
          denom: upokt
        proof_missing_penalty:
          amount: "320000000"
          denom: upokt
        proof_submission_fee:
          amount: "1000000"
          denom: upokt
    session:
      params:
        num_suppliers_per_session: 15
    tokenomics:
      params:
        mint_allocation_percentages:
          dao: 0.1
          proposer: 0.05
          supplier: 0.7
          source_owner: 0.15
          application: 0.0
        # The dao reward address SHOULD match that of the "pnf" below (i.e. `make poktrolld_addr ACC_NAME=pnf`).
        # This is the address that will receive the dao/foundation rewards during claim settlement (global mint TLM).
        # TODO_MAINNET(@olshansk): Consolidate the usage of DAO/PNF throughout the configs & codebase.
        dao_reward_address: "pokt1f0c9y7mahf2ya8tymy8g4rr75ezh3pkklu4c3e"
    shared:
      params:
        num_blocks_per_session: 10
        grace_period_end_offset_blocks: 1
        claim_window_open_offset_blocks: 1
        claim_window_close_offset_blocks: 4
        proof_window_open_offset_blocks: 0
        proof_window_close_offset_blocks: 4
        supplier_unbonding_period_sessions: 1
        application_unbonding_period_sessions: 1
        compute_units_to_tokens_multiplier: 42
```
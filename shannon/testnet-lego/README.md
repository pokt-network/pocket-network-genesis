# Pocket Network Shannon Testnet <!-- omit in toc -->

- [Accounts](#accounts)
- [Seeds](#seeds)
- [Private keys](#private-keys)
- [Ignite config.yaml](#ignite-configyaml)

## Accounts

- **DAO/PNF**: `pokt1f0c9y7mahf2ya8tymy8g4rr75ezh3pkklu4c3e`
- **Faucet**: `pokt1fpxstscnqtzc9tq0u0nlvg69hqt6zhaxyka2mj`
- **Validator1**: `pokt1sadgp3998r2wxka9ec88hm0znxumr4m7wh49x5`
- **Validator2**: `pokt14kgy84sgl6a6e4kk8hn3e8gj3c3spk6jwh2q64`
- **Validator3**: `pokt18rdpjl3ndma372h4503ug8cpd6kzwr8hted8wy`
- **Validator4**: `pokt1u994thderhxj60pwhjscne8wcfn8efc8w2020j`
- **Validator5**: `pokt1ay694phar5wwsvmedyhmmxh08gjwc2vm4qxtsj`

## Seeds

Currently supported list of seed nodes can be found in the [seeds](./seeds) file.

## Private keys

The TestNet is currently maintained by Grove.

Information on how to get access to keys can be found [on Notion here](https://www.notion.so/buildwithgrove/Beta-TestNet-144a36edfff6802597a1fa4c39ef3fcb?pvs=4). Please request access if you
believe you need it.

## Ignite config.yaml

The following [Ignite CLI](https://github.com/ignite/cli) config was used to
generate the genesis file for the Shannon Beta TestNet.

```yaml
version: 1
build:
  main: cmd/pocketd
  binary: pocketd
accounts:
  - name: faucet
    coins:
      - 9999999999999999999999999999999999999999999999999999999999999999upokt
  - name: pnf
    address: "pokt1f0c9y7mahf2ya8tymy8g4rr75ezh3pkklu4c3e"
    coins:
      - 69000000000000000000042upokt
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
faucet:
  name: faucet
  coins:
    - 10000upokt
client:
  typescript:
    path: ts-client
  hooks:
    path: react/src/hooks
  openapi:
    path: docs/static/openapi.yml
validators:
  - name: validator1
    bonded: 1000000000000000upokt

    app:
      telemetry:
        enabled: true
      pocket:
        telemetry:
          cardinality-level: high
      api:
        swagger: true
    config:
      moniker: "validator1"
      consensus:
        timeout_commit: "5m"
        timeout_propose: "5m"
      instrumentation:
        prometheus: true
      log_level: "info"

      rpc:
        max_body_bytes: "100000000"
      mempool:
        max_tx_bytes: "100000000"
    client:
      chain-id: pocket-beta

genesis:
  app_name: pocket
  chain_id: pocket-beta
  app_state:
    mint:
      params:
        mint_denom: upokt

        inflation_rate_change: "0.0"
        inflation_max: "0.0"
        inflation_min: "0.0"

    staking:
      params:
        bond_denom: upokt
        max_validators: 10
    crisis:
      constant_fee:
        amount: "10000"
        denom: upokt
    gov:
      params:
        min_deposit:
          - amount: "1000000000000000"
            denom: upokt

    application:
      params:
        max_delegated_gateways: "7"
        min_stake:
          amount: "100000000"
          denom: upokt
      applicationList: []

    supplier:
      params:
        min_stake:
          amount: "1000000"
          denom: upokt

        staking_fee:
          amount: "1"
          denom: upokt
      supplierList: []

    gateway:
      params:
        min_stake:
          amount: "1000000"
          denom: upokt
      gatewayList: []

    service:
      params:
        add_service_fee:
          amount: "1000000000"
          denom: upokt
        target_num_relays: 100000
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

        dao_reward_address: "pokt1eeeksh2tvkh7wzmfrljnhw4wrhs55lcuvmekkw"
        global_inflation_per_claim: 0.1

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
        gateway_unbonding_period_sessions: 1
        compute_units_to_tokens_multiplier: 42
```

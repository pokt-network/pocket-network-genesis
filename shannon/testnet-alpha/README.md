# Pocket Network Shannon Testnet <!-- omit in toc -->

- [Accounts](#accounts)
- [Seeds](#seeds)
- [Private keys](#private-keys)
- [Ignite config.yaml](#ignite-configyaml)

## Accounts

- **DAO/PNF**: `pokt1r6ja6rz6rpae58njfrsgs5n5sp3r36r2q9j04h`
- **Faucet**: `pokt1v3mcrj0h2zfekyf2n8m369x4v9wfvdm34hecd9`
- **Validator1**: `pokt19uwrjhyamhvnjm5edwccmfgvvkscnuqhkv2egz`

## Seeds

Currently supported list of seed nodes can be found in the [seeds](./seeds) file.

## Private keys

The TestNet is currently maintained by Grove.

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
      - 999999999999999999upokt
  - name: pnf
    coins:
      - 69000000000000000000042upokt
  - name: validator1

    coins:
      - 900000000000000upokt
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
    bonded: 1000000000upokt

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
        timeout_commit: "60s"
        timeout_propose: "60s"
      instrumentation:
        prometheus: true
      log_level: "info"

      rpc:
        max_body_bytes: "100000000"
      mempool:
        max_tx_bytes: "100000000"
    client:
      chain-id: testnet-alpha

genesis:
  app_name: pocket
  chain_id: testnet-alpha
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

        max_validators: 1
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

# clone-lin-gmx-v2-swap-inventory

Experimental LIN clone of GMX V2 `applyDeltaToVirtualInventoryForSwaps` (uint64-scale unsigned long-token / short-token swap virtual inventory, floor-at-zero).

- **Upstream:** [gmx-io/gmx-synthetics](https://github.com/gmx-io/gmx-synthetics) `contracts/market/MarketUtils.sol` commit `a85ea3491c19c93bb4b5a002d9b358fb769b7849` (GPL-2.0-or-later after BUSL Change Date 2026-08-31).
- **LIN kernel:** [`src/lin_gmx_v2_swap_inventory.lin`](src/lin_gmx_v2_swap_inventory.lin)
- **C11 oracle copy:** [`test/oracles/gmx_v2_swap_inventory_c11.c`](test/oracles/gmx_v2_swap_inventory_c11.c)
- **Proofs (lin-open only):** [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open) `examples/gmx_v2_swap_inventory/` and `python3 test/prove_gmx_v2_swap_inventory_external.py`
- **Class:** EXPERIMENTAL. Not Arbitrum GMX V2 uint256. Not a production replacement. Not `applyDeltaToVirtualInventoryForPositions` (signed single) and not `applyDeltaToOpenInterest` (unsigned OI + signed long-flipped VI).

Named goldens (uint64-scale, long=1e8 short=5e7): long-token +3e7 → long **130000000** / short **50000000** vs both-sides short **80000000** vs position-style flip **70000000**; short-token +3e7 → short **80000000**; long -1.5e8 **floors 0** vs reject-uint **ok=0** vs signed **-50000000**; missing virtual market leaves the pair and returns nextValue **0**; unexpected token with no virtual market **ok=1** vs token-first **ok=0**; 7e18+3e18 fail-closes vs naive i64 wrap **-8446744073709551616**.

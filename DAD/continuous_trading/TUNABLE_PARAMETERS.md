# Tunable Parameters in trader.py - Complete Reference

## OSMIUM (Market-Making Strategy)

### 1. **OSMIUM_EMA_ALPHA** (Line 230)
- **Current**: 0.15
- **Range**: 0.10 - 0.25
- **Impact**: Controls trend detection speed
  - 0.10 = Very slow, ignores noise
  - 0.15 = Balanced (current, Phase 2 optimal)
  - 0.25 = Faster, more responsive but noisier
- **When to adjust**: If market-making quotes are too slow to respond

### 2. **OSMIUM_VWAP_WINDOW** (Line 231)
- **Current**: 15
- **Range**: 10 - 25
- **Impact**: Number of trades used to calculate VWAP (fair value anchor)
  - 10 = Super responsive, noisy
  - 15 = Balanced (current, Phase 2 optimal)
  - 25 = Very smooth, slower adaptation
- **When to adjust**: If fair value estimates are too volatile or too stale

### 3. **OSMIUM_INVENTORY_BIAS** (Line 232)
- **Current**: 0.7
- **Range**: 0.5 - 1.0
- **Impact**: How aggressively to rebalance position back to zero
  - 0.5 = Very aggressive rebalancing
  - 0.7 = Balanced (current, Phase 2 optimal)
  - 1.0 = Very conservative, allow position drift
- **When to adjust**: If hitting position limits too often or not using limits effectively

### 4. **OSMIUM_VOL_BASE** (Line 233)
- **Current**: 20
- **Range**: 15 - 30
- **Impact**: Volatility threshold for position scaling
  - Lower = More sensitive to volatility changes, smaller positions
  - 20 = Balanced (current, Phase 2 optimal)
  - Higher = Less sensitive, maintains larger positions
- **When to adjust**: If volatility scaling is too aggressive or too passive

### 5. **MAX_DISTANCE** (Line 250)
- **Current**: 20
- **Range**: 15 - 30
- **Impact**: Safety check - prevents trading when price deviates too far from fair value
  - 15 = Strict, fewer extreme orders
  - 20 = Balanced (current)
  - 30 = Permissive, allows wider moves
- **When to adjust**: If rejecting profitable orders or accepting bad ones

---

## PEPPER (Trend-Following Strategy)

### 6. **PEPPER_EMA_ALPHA** (Line 325)
- **Current**: 0.3
- **Range**: 0.25 - 0.40
- **Impact**: Controls trend detection responsiveness
  - 0.25 = Slower, fewer false signals but misses trends
  - 0.3 = Balanced (current, Phase 2 optimal)
  - 0.40 = Faster, catches trends quicker but more whipsaws
- **When to adjust**: If trend signals are lagging or generating false signals

### 7. **PEPPER_VOL_BASE** (Line 326)
- **Current**: 300
- **Range**: 250 - 350
- **Impact**: Volatility threshold for PEPPER position scaling
  - 250 = More aggressive scaling
  - 300 = Balanced (current, Phase 2 optimal)
  - 350 = More conservative scaling
- **When to adjust**: If order sizes are too large or too small

---

## Position Limits (Already Testing via comprehensive_testing.py)

### **OSMIUM_POSITION_LIMIT**
- **Current**: ±80 (Phase 2 optimal) or ±90 (Grid search best)
- **Range**: ±40 - ±100

### **PEPPER_POSITION_LIMIT**
- **Current**: ±80 (Phase 2 optimal) or ±90 (Grid search best)
- **Range**: ±40 - ±100

---

## Parameter Tuning Strategy

### Phase 2 (Already Completed)
- Tested 2,304+ combinations
- Settled on current values as optimal
- Used grid search approach

### Phase 3 (What You're Doing Now - 100 Loops)
- Test position limits with realistic order matching
- Test with market randomization (changing conditions)
- Identify if any position limit combo beats Phase 2

### Phase 4 (Future - Optional Parameter Grid)
Could test combinations of:
- EMA Alpha variations (±0.05 from current)
- VWAP Window variations (±5 from current)
- Inventory Bias variations (±0.15 from current)

---

## Current Status (Phase 2 Validated)

All parameters are currently **locked and validated**:

✅ OSMIUM_EMA_ALPHA = 0.15 (proven optimal)
✅ OSMIUM_VWAP_WINDOW = 15 (proven stable)
✅ OSMIUM_INVENTORY_BIAS = 0.7 (proven conservative)
✅ OSMIUM_VOL_BASE = 20 (proven balanced)
✅ PEPPER_EMA_ALPHA = 0.3 (proven responsive)
✅ PEPPER_VOL_BASE = 300 (proven adaptive)

Position limits: ±80/±80 (Phase 2) or ±90/±90 (New potential best)

---

## Loop Testing Focus (Current Work)

You're currently testing:
- **Variables**: Position limits (10 configurations)
- **Market Conditions**: Randomized order + price noise (100 loops each)
- **Goal**: Find if any position limit combo outperforms Phase 2 under realistic matching

---

## If You Want to Test Parameter Combinations Too

You could create an extended grid that tests:
```
Position Limits (10) × EMA Alpha (3) × VWAP Window (3) × Inventory Bias (3) = 270 combinations
Each × 100 loops = 27,000+ total backtests
Time: 8-12 hours
```

Would you like a script for this, or stick with position limit testing first?


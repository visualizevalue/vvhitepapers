# Checks: A Protocol for Bottom-Up Verification

## Abstract

Checks is a generative art protocol that explores emergent value creation through participant-driven scarcity mechanisms. Launched as an open edition of 16,031 identical NFTs, the system implements a compositing architecture that enables token holders to irreversibly transform their assets through on-chain burning operations. This paper presents the technical implementation and game-theoretic implications of a system where verification is earned through demonstrated commitment rather than assigned by centralized authority.

### Checks Editions

**Artist**: Jack Butcher
**Contract**: `0x34eEBEE6942d8Def3c125458D1a86e0A897fd6f9`
**Launch**: January 2023

### Checks Originals

**Artists**: Jack Butcher, Jalil Wahdatehagh
**Contract**: `0x036721e5A769Cc48B3189EFbb9ccE4471E8A48B1`
**Launch**: February 2023

---

## 1. Introduction

The checkmark symbol (✓) represents verification, approval, and authenticity. Traditional verification systems operate through centralized gatekeepers who grant status from positions of authority. This paper presents an alternative model: verification earned through irreversible on-chain actions.

Checks implements a protocol where value and scarcity emerge entirely from participant decisions. Unlike traditional NFT projects that assign rarity at genesis, this system begins with complete equality—16,031 identical tokens—and enables holders to create differentiation through permanent token burns.

### 1.1 Value Assignment Models

This protocol contrasts two approaches to value creation in digital assets:

**Centralized Value Assignment**

- Scarcity predetermined by creator
- Rarity assigned at token genesis
- Participants receive fixed attributes
- Value hierarchy established top-down

**Decentralized Value Emergence**

- Scarcity emerges from participant actions
- Rarity created through irreversible operations
- Participants transform token properties
- Value hierarchy established bottom-up

Checks implements the latter model as a functional system demonstrating emergent verification.

### 1.2 Protocol Objectives

1. Enable participant-driven rarity creation through token burns
2. Implement verifiable scarcity via immutable on-chain operations
3. Create game-theoretic dynamics that incentivize strategic decision-making
4. Demonstrate that verification can be earned rather than granted

---

## 2. Protocol Architecture

### 2.1 Genesis State

The protocol launched with 16,031 identical ERC-721 tokens. Each token shared:

- Identical visual representation (80 checkmarks in grid formation)
- Identical metadata
- Identical on-chain properties
- Equal starting position with zero predetermined rarity hierarchy

This egalitarian initialization was necessary to demonstrate pure emergent differentiation. Any initial variation would constitute top-down value assignment, undermining the protocol's core thesis.

### 2.2 Migration Mechanism

A two-phase architecture separates static editions from dynamic originals:

**Phase 1: Editions** (Contract: `0x34eE...d6f9`)

- Static ERC-721 tokens
- Immutable visual and metadata properties
- Serves as historical artifact of genesis state

**Phase 2: Originals** (Contract: `0x0367...8B1`)

- Dynamic ERC-721 tokens with compositing capabilities
- Implements transformation functions
- Maximum supply: 8,015 (migrated from burned Editions)

### 2.3 Core Operations

The protocol implements three transformation primitives:

#### 2.3.1 Composite Operation

```solidity
function composite(uint256 tokenId, uint256 burnId, bool swap) external
```

The composite operation combines two tokens of equivalent rarity tier through permanent burn:

**Requirements:**

- Both tokens must share identical `divisorIndex` (rarity tier)
- Caller must own or be approved for both tokens
- Tokens cannot be identical (self-compositing prohibited)

**State Transitions:**

- Token A (n checks) + Token B (n checks) → Token A (n/2 checks)
- Token B permanently burned
- Token A records Token B's ID in composite history
- Visual properties undergo genetic recombination

**Progression Sequence:**

```
80 + 80 → 40
40 + 40 → 20
20 + 20 → 10
10 + 10 → 5
5 + 5 → 4
4 + 4 → 1
```

#### 2.3.2 Sacrifice Operation

```solidity
function inItForTheArt(uint256 tokenId, uint256 burnId) external
```

The sacrifice operation transfers visual genome without altering rarity tier:

**Mechanism:**

- Burns one token to extract its visual properties
- Transfers complete color palette and gradient configuration
- Preserves recipient token's `divisorIndex` (rarity unchanged)
- Updates recipient's birth timestamp

This operation enables aesthetic optimization independent of scarcity progression.

#### 2.3.3 Infinity Operation

```solidity
function infinity(uint256[] calldata tokenIds) external
```

The infinity operation represents the terminal compositing state:

**Requirements:**

- Exactly 64 input tokens
- All tokens must have `divisorIndex = 6` (single-check state)
- Caller must control all input tokens

**Execution:**

- 63 tokens permanently burned
- First token in array transitions to `divisorIndex = 7` (infinity state)
- Visual representation changes to solid black
- Check count displays as ∞

**Total Burn Requirement:** Creating one infinity token requires 4,096 genesis-state (80-check) tokens, representing 51.1% of maximum supply.

### 2.4 Rarity Tier Structure

| Tier | Checks Count | DivisorIndex | Burns Required | Cumulative Burns |
| ---- | ------------ | ------------ | -------------- | ---------------- |
| 0    | 80           | 0            | 0              | 0                |
| 1    | 40           | 1            | 1              | 1                |
| 2    | 20           | 2            | 2              | 3                |
| 3    | 10           | 3            | 4              | 7                |
| 4    | 5            | 4            | 8              | 15               |
| 5    | 4            | 5            | 16             | 31               |
| 6    | 1            | 6            | 32             | 63               |
| 7    | ∞            | 7            | 4,096          | 4,095            |

Each tier requires exponentially increasing commitment, creating provable scarcity through demonstrated action.

---

## 3. Theoretical Framework

### 3.1 Bottom-Up Verification Model

Traditional verification systems operate through authority-based credentialing. A central entity declares certain attributes valid, and participants accept this declaration. The Checks protocol inverts this model.

**Verification Properties:**

- **Earned, not granted**: Rarity achieved through irreversible operations
- **Transparent**: Complete burn history stored on-chain
- **Immutable**: Past actions cannot be revised or revoked
- **Permissionless**: No gatekeeper controls access to transformation

A 1-check token is not rare by declaration—it is rare because its holder provably burned 63 other tokens. The scarcity is verifiable through blockchain state, not asserted by authority.

### 3.2 Value Creation Through Destruction

The protocol implements a paradox: to create value, participants must destroy value.

**Mechanism:**

- Increasing rarity requires burning 50% of holdings per tier
- Maximum rarity (∞) requires burning 99.98% of input tokens
- All burns are permanent and irreversible

**Implications:**

- Commitment is costly and provable
- Rarity signals demonstrated sacrifice, not luck
- Value creation requires skin in the game

This mechanism ensures that scarcity is earned through economic commitment rather than randomly assigned.

### 3.3 Emergent vs. Predetermined Scarcity

Most NFT protocols assign rarity distributions at genesis. Checks implements emergent scarcity:

**Predetermined Model (Traditional):**

- Creator defines rarity at launch
- Distribution fixed and immutable
- Participants receive random allocations
- Supply curve known in advance

**Emergent Model (Checks):**

- All tokens identical at genesis
- Rarity develops through participant actions
- Distribution evolves dynamically
- Final state unknowable at launch

If no participant composites, all tokens remain equal. If all participants composite maximally, supply collapses toward theoretical minimum. The actual outcome depends entirely on decentralized decision-making.

---

## Technical Implementation

### Fully On-Chain

Everything needed to render a Check exists permanently on Ethereum:

- Visual generation (SVG)
- Metadata (JSON)
- Color palettes
- Transformation history

No IPFS. No external servers. The artwork is the blockchain state.

### The Epoch System: Fair Randomness

Each Check gets random visual properties (colors, gradients). But blockchain randomness is manipulable. The solution: commit-reveal.

**Phase 1: Commitment**
First action in an epoch commits to a future block (50 blocks ahead).

**Phase 2: Reveal**
After that block arrives, randomness is derived from the blockhash — unpredictable at commitment time.

**Phase 3: Application**
All Checks in that epoch use this randomness.

Result: nobody can game the visual properties. Fair distribution of aesthetics across participants.

### Visual Genetics

When two Checks composite, their colors don't simply transfer — they breed:

- Gradient inheritance (20% chance to force parent gradient)
- Color band mixing (averages of both parents)
- Color selection from combined pools

Each composite creates genuinely new visual combinations while maintaining genetic lineage.

### Complete Provenance

Every Check carries its full transformation history on-chain:

```solidity
struct StoredCheck {
    uint16[6] composites;  // Family tree of burned parents
    uint8[5] colorBands;   // Color evolution across generations
    uint8[5] gradients;    // Gradient evolution
    uint8 divisorIndex;    // Current rarity tier
    uint32 epoch;          // Birth epoch
    uint16 seed;           // Unique identifier
    uint24 day;            // Creation date
}
```

You can trace every Check back through every burn that created it. Complete, immutable, on-chain provenance.

---

## Game Theory & Dynamics

### The Composite Dilemma

Every holder faces a continuous choice:

**Hold**: Token may appreciate as others burn supply
**Composite**: Create rarer token but destroy half your holdings
**Sacrifice**: Optimize aesthetics at the cost of quantity

There's no objectively correct answer. The decision depends on:

- Your belief about others' compositing behavior
- The current supply distribution
- Your aesthetic preferences
- Your time horizon

This creates genuine strategic depth. Each burn changes the landscape for all participants.

### The Coordination Problem

Creating a Black Check (∞) requires either:

- One participant acquiring and burning 4,096 Originals (estimated ~$200k+ at moderate floor prices)
- 64 participants each contributing one single-check token and coordinating to execute

This is game theory in action: massive individual commitment or complex multi-party coordination, both with uncertain outcomes.

The first Black Check hasn't been created yet. Will it ever be? What will it be worth? These questions remain open.

### Supply Destruction Economics

The system is deflationary by design:

- Maximum possible Originals: 8,015
- Every composite burns one token
- Creating ∞ burns 4,095 tokens
- Current supply continuously decreasing

As supply falls, each remaining token represents a larger fraction of the total. But compositing requires destroying tokens to create rarity. The tension between holding and burning drives the entire economic system.

---

## What Checks Proves

### 1. Value Can Be Bottom-Up

Traditional NFTs: creator assigns rarity → participants receive it
Checks: participants begin equal → create rarity through action

The experiment shows that value doesn't require top-down declaration. It can emerge entirely from participant choices and demonstrated commitment.

### 2. Verification Can Be Earned

The checkmark traditionally means "verified by authority." Checks asks: what if verification meant "verified by sacrifice"?

A 1-check token isn't rare because someone declared it rare. It's rare because someone burned 63 tokens to create it. The rarity is verifiable, permanent, and earned.

### 3. On-Chain Mechanics Can Be The Art

The compositing system isn't infrastructure for art — it is the art. The smart contracts encode the conceptual framework. Interacting with the system is participating in the artwork.

Every burn is a creative act. Every composite changes the piece. The artwork isn't finished — it evolves with each participant decision.

### 4. Permanence Enables Meaning

Because burns are irreversible and on-chain:

- Commitments are credible
- History is immutable
- Actions have weight
- Decisions matter

This permanence is what allows bottom-up verification to function. Without it, the system would collapse into signaling without substance.

---

## The Artwork

At its core, Checks asks:

**What is verification in the internet age?**

When anyone can claim anything, when credentials can be purchased, when status is mediated through platforms — what does verification mean?

Checks proposes an answer: verification through demonstrated commitment. Through permanent, on-chain sacrifice. Through actions that cannot be undone.

The checkmark doesn't certify that an authority approved you. It certifies that you were willing to destroy value to create it.

This is verification from the bottom up. Not granted, but earned. Not declared, but proven.

---

## Technical Specifications

### Contract Information

**Network**: Ethereum Mainnet
**Standard**: ERC721 (modified)
**Solidity Version**: ^0.8.17
**License**: MIT

### Key Functions

```solidity
// Migration from Editions to Originals
function mint(uint256[] calldata tokenIds, address recipient) external

// Visual transfer without compositing
function inItForTheArt(uint256 tokenId, uint256 burnId) external

// Composite two tokens
function composite(uint256 tokenId, uint256 burnId, bool swap) external

// Create the Black Check
function infinity(uint256[] calldata tokenIds) external

// Standard burn
function burn(uint256 tokenId) external

// Epoch management
function resolveEpochIfNecessary() public

// View functions
function getCheck(uint256 tokenId) external view returns (Check memory)
function svg(uint256 tokenId) external view returns (string memory)
function tokenURI(uint256 tokenId) public view returns (string memory)
```

### Core Events

```solidity
event Sacrifice(uint256 indexed burnedId, uint256 indexed tokenId);
event Composite(uint256 indexed tokenId, uint256 indexed burnedId, uint8 indexed checks);
event Infinity(uint256 indexed tokenId, uint256[] indexed burnedIds);
event NewEpoch(uint256 indexed epoch, uint64 indexed revealBlock);
```

---

## Resources

**Checks Website**: [https://checks.art/](https://checks.art/)
**Editions Contract**: [0x34eEBEE6942d8Def3c125458D1a86e0A897fd6f9](https://etherscan.io/address/0x34eEBEE6942d8Def3c125458D1a86e0A897fd6f9)
**Originals Contract**: [0x036721e5A769Cc48B3189EFbb9ccE4471E8A48B1](https://etherscan.io/address/0x036721e5A769Cc48B3189EFbb9ccE4471E8A48B1)

---

## Artist's Note

**This artwork may or may not be notable.**

It questions:

- Is verification self-declared or externally granted?
- Does asserting notability make it so?
- Can bottom-up verification work?

The answer depends on what participants choose to do. Every burn is a vote. Every composite is an answer.

---

_Version 1.0 — October 2025_

_This describes an experimental artwork exploring value creation, verification, and on-chain commitment. Nothing herein constitutes financial, legal, or investment advice. All compositing actions are irreversible. This artwork may or may not be notable._

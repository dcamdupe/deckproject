# Low-Level Timber Deck, Sydney NSW

A planning and design record for a low-level timber deck beside a house. It captures the project brief, the information provided, the decisions made so far, and what is still open. It is intended as the starting context for continuing the work in Claude Code.

## 1. Project summary

- **Location:** Sydney, NSW, Australia.
- **What:** A low-level, single-layer timber deck running alongside the side of a house.
- **First section size:** 1874 mm wide x 3000 mm long.
- **Height:** Less than 1 m above ground (stated by the owner).
- **Structural post:** A 90 x 90 mm post passes through the deck and supports the level above. It is not an edge post for the deck.
- **Future work (the owner has said these come later):**
  - Steps. There will be several, for example a 2 m first deck section, a step down to a 1 m section, then more steps.
  - Deck posts, footings and stirrups.
  - More detail added to the drawing over time.
- **Use case:** A push lawnmower will be moved up and down the steps, so the step edges need protection (ramps were discussed).
- **Reference the owner used:** Bunnings Workshop discussion 45715 (low-level, single-layer deck).

## 2. Key information provided by the owner

| Item | Value |
|---|---|
| Deck width | 1874 mm |
| Deck length | 3000 mm |
| Joist direction | Run left to right in the top view, across the 1874 mm width as drawn |
| Framing strategy | Single layer: bearers under the joists, with joists continuous on top |
| Structural post size | 90 x 90 mm |
| Structural post position | 2250 mm from the top of the deck, 258 mm from the right-hand side |
| Council approval | Owner states the deck is under 1 m high |
| Stirrup style being considered | Pryda full stirrup post anchors (for example 65x90 mm M10, and the high-wind 600x90 mm M12) |

## 3. Decisions made

### 3.1 Framing and layout

- **Joists:** 90 x 45 mm at no more than 450 mm centres.
  - 8 full-length joists plus one short joist (6a) beside the structural post.
  - Joist centre positions: 22.5, 495.5, 923.5, 1351.5, 1779.5, 2207.5, 2555.4 and 2977.5 mm.
  - Joist 6 is set 20 mm clear of the post's top face. Joists 2 to 5 are spread evenly between the joist 1 doubler and joist 6: 383 mm clear gaps, 428 mm centres.
  - Joists 7 and 8 stay on the original 422.14 mm grid. Joist 6 to 7 is 347.9 mm centres.
  - Joist 6a is a short joist 20 mm clear of the post's bottom face (centre 2382.5 mm), running from the central bearer to the right edge, 959.5 mm long.
  - Joist 1 is a double joist: a second 90 x 45 mm member fixed against its inward face (occupying 45 to 90 mm), so 9 joist lengths in total. No other joist moves.
- **Bearers:** 3 bearers, 140 x 45 mm (assumed size), under the joists.
  - Bearer centres: 22.5, 937 and 1851.5 mm, about 914.5 mm apart.
  - This is within the roughly 1000 mm span guide for a 90 x 45 mm joist.
- **Joists sit on top of the bearers** and are continuous. The earlier plan of bearers beside the joists was dropped.
- **Structural post:** The post is not moved to suit the framing. The joists are laid out around it (joist 6 and short joist 6a sit 20 mm either side); no bearer moves.
  - Post occupies x 1526 to 1616 mm from the left and y 2250 to 2340 mm from the top.
  - Clearances: 20 mm to joist 6 (above), 20 mm to joist 6a (below), 213 mm to the right bearer, 566.5 mm to the centre bearer.
  - The post sits between joists 6 and 6a.
- **Deck posts:** 9 posts, 90 x 90 mm (assumed size), three under each bearer.
  - Along the length: centres at 45, 1500 and 2955 mm from the top, so the bearers span 1455 mm between post centres. This span is not yet checked against AS 1684.
  - Across the width: centres at 45, 937 and 1829 mm from the left. Edge posts are kept flush inside the deck outline rather than centred on the edge bearers.
  - Height, footings and stirrups are still open.
- **Decking boards** run towards the steps. Whether to add a boards-at-90-degrees edge for the step is a step-stage decision still to be made.

### 3.2 Posts, footings and treatment

- **Stirrups:** Bolt-down or cast-in stirrups are the approach being considered for deck posts, with the stirrup at least 75 mm above finished ground.
  - An earlier statement of 30 to 50 mm above concrete was wrong and has been corrected.
- **Treatment class:** H4 versus H5 was discussed. H5 is the heavier treatment for in-ground or severe-decay contact. Check AS 1604 and the supplier's tags before buying.
- **Posts against a house:** The question of attaching to the house versus concreting posts in was discussed for the deck's supporting posts, not the structural post.

### 3.3 Approvals and clearances

- The owner says the deck is under 1 m. In NSW the deck floor height must be at most 1 m, among other criteria, to qualify as exempt or complying development. Check the NSW Planning Portal for the full criteria.
- Under-floor clearance and subfloor ventilation are driven by the NCC (150 mm clearance, more for termite inspection). This still needs to be confirmed for this site.

### 3.4 Drawing conventions

- Top view on the left. Side view on the right, looking from the right-hand edge with up to the left, so joist ends are nearest the top view and the bearer is beyond.
- Both views share the vertical scale so the joist rows align.
- Nothing in the drawing is configurable unless the owner asks. The only toggles are Joists, Bearers, Deck posts and Structural post.
- No inputs and no layers for joist numbers, dimensions or bearer lines.

## 4. The interactive drawing

An interactive SVG page was built and published as a private artifact (Version 6). Its source is a single HTML file with a JavaScript IIFE that generates the SVG.

- **Features:** top and side views, show/hide toggles (Joists, Bearers, Deck posts, Structural post), hover/tap/focus readouts for joists, bearers, deck posts and the structural post, summary chips, light and dark themes, IBM Plex fonts, aria labels.
- **Key constants:**

```js
var P = { W: 1874, L: 3000, t: 45, d: 90, maxC: 450, nb: 3, bt: 45, bd: 140, ps: 90, pt: 2250, pr: 258, pg: 20, dbl: [0], dps: 90, npp: 3 };
var K = 0.27, OX = 176, OY = 74, SX = 748, VBW = 900, GUIDE_SPAN = 1000;
```

- **Layout maths:**
  - Joist grid: `n = ceil((L - t) / maxC)`, centres `c = (L - t) / n`. The last grid joist above the post is then moved to `pg` clear of it, and the joists before it are spaced with equal clear gaps.
  - Bearer spacing: `s = (W - bt) / (nb - 1)`.
  - Post left edge: `postX = W - pr - ps = 1526`.
- **Not yet checked:** the rendered page has never been inspected visually. Its script passed a syntax check only.

## 5. Assumptions and caveats

- Joist and bearer sizes and spans come from community guidance (joists at 450 mm centres or closer, a 90 x 45 mm joist spanning about 1000 mm). They are not taken from AS 1684 span tables.
- Bearer size (140 x 45 mm) is an assumption.
- Before building, confirm member sizes, spans, fixings and footings against AS 1684 and the supplier's span tables, or with a builder or engineer.
- Confirm the load path for the 90 x 90 mm structural post (what it carries and what it bears on). This is not the deck framing's job, and the post should not rely on the deck for support.
- Council and planning rules should be confirmed on the NSW Planning Portal for the actual site.

## 6. Open questions and next steps

1. Steps: layout, riser and tread sizes, board direction, and edge treatment.
2. Deck posts, footings and stirrup selection, and how posts and joists are managed across the stepped sections.
3. Final member sizes and spans confirmed against AS 1684.
4. Under-floor clearance, subfloor ventilation and termite inspection access.
5. Lawnmower access and edge protection (ramp options).
6. Visual check of the drawing, then extend it with steps and footings.

## 7. Suggested repository layout

```
project.md          this file
drawing/            interactive SVG deck-frame page (HTML)
```

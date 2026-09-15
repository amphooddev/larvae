# amphoodcoinrh

A real fruit amphood brain, simulated neuron by neuron,

165,122 neurons. 10,228,000 signed synaptic connections. Every one of them
measured from an actual male *Drosophila melanogaster* by electron microscopy —
not invented, not sampled from a distribution, not a neural network "inspired
by" a brain.


## What it actually does

Press START and a real Chromium opens ponsfamily.com/launchpad. Its screenshots
are sampled through the amphood's **892 retinotopic hex columns** into L1 and L2 —
the lamina monopolar cells that are the direct postsynaptic targets of
photoreceptors R1–R6. 165,122 neurons integrate. The cursor comes back out of
the descending neurons a amphood actually walks with:

| neuron | what it does in a amphood | what it does here |
|---|---|---|
| **DNa02** left vs right | steering — a amphood turns by left/right asymmetry | cursor x |
| **DNa01** | forward walking | cursor y |
| **MDN** | the Moonwalker descending neuron — walking backwards | reverse |
| **DNp09** | stopping | the click |

Then it connects the wallet, accepts the launchpad's terms, uploads the token
image, fills the form — name, ticker, description and the `x.com/` handle —
picks the paired asset out of a 57-item list of tokenised equities, opens
**Advanced**, sets the creator tax, and launches.

## The amphood is loose on the internet

`roam.py` gives it a browser and no instructions. A page is screenshotted,
sampled through the 892 hex columns, and 165,122 neurons decide where the
cursor goes. If a click lands on a link, the amphood is somewhere new. When its
forward drive pushes past the bottom of the window the page scrolls, so it
walks down a page the way it walks across one.

It is watchable live at **[https://amphood.site/](https://amphood.site/)** — the
page it is looking at, the neurons firing, and what its descending neurons are
doing, all read out of the running simulation.

```bash
py roam.py            # http://localhost:4660, no start button
```

There is no start and no stop. It roams when the process is up, and if a run
dies it waits six seconds and starts another life.

### The rails, and why each one is there

A random clicker on the open internet, streamed publicly, from a machine that
also holds a funded wallet, is a genuinely bad idea unless it is fenced.

- **No wallet.** This browser gets no key, no provider and no extension. The
  roaming browser and the launching browser share nothing but the brain.
- **No keyboard.** The amphood cannot type, so it cannot fill a field, write a
  message or answer a prompt.
- **Every click is checked before it lands.** Anything that reads as a submit,
  an upload, a payment or a sign-in is vetoed, and the veto count is on screen.
- **A domain fence.** The first thing built was a keyword blocklist; the first
  thing tested was `p0rn.com`, which walked straight through it. Keyword
  filters do not hold, so the real control is an allowlist of link-rich
  domains. `amphood_ROAM_OPEN=1` removes the fence and should not be left on for an
  unattended public stream.
- No downloads, no popups, no dialogs, and a hop budget so a dead end does not
  become a permanent home.

### What the readouts actually are

Nothing on that page is decoration. `amphoodsim` was extended to report it:

| on screen | what it is |
|---|---|
| neurons firing | a per-neuron bit set on every spike in the window |
| spikes/sec | total spikes divided by simulated time |
| membrane | mean membrane potential at the end of the window |
| visual / motor | firing neurons intersected with L1/L2 and the DN groups |
| the scatter | those neurons at their **measured soma coordinates** |
| DNa02 / DNa01 / MDN / DNp09 | the recorded rates already driving the cursor |

`amphoodPilot.step(detail=True)` returns the extra readout as a fifth value, so
every existing caller still unpacks four and is unaffected.

The site itself is in `site/` — a static page on Vercel plus one serverless
function that proxies the chain, because the public Robinhood node
intermittently answers `Access-Control-Allow-Origin: *,*`, which browsers
refuse. The live feed comes from the hosted roaming service over a websocket;
if that service is unreachable the page falls back to a published tunnel address.


### The voice

The amphood has no language, so its journal is written for it, and `voice.py` is
the writer. Observe: pull `/state` from the live roamer, the live token page
and the on-chain launch constants into one packet. Read: fetch a short
allowlist of real pages (its own token page, its own site, the pages the amphood
itself walked through, and a few reference pages on memecoins and tokenised
stocks) and pass excerpts in. Write: a language model drafts a first-person
entry from that packet and nothing else. Check: every number in the draft must
appear in the packet, and any trading or hype language fails it; a rejected
draft is dropped, there is no second draft, and nothing edits the text. What
it keeps in its journal is checked the same way before it is kept. Post,
through `xpost.py`, which records every post before it is sent, caps posts
per day and refuses repeats and near-repeats. There is no command that posts
text by hand: the only route to the amphood's account is a draft that passed the
check. The offline `stub` model, used by the tests, writes to its own journal
and can never post. Two things in this project are invented, and both are
labelled: the reward signal in the mushroom body, and the words. Everything
else is a measurement.

```bash
py voice.py --once --dry      # observe, read, write one entry; post nothing
py voice.py --loop            # every amphood_VOICE_EVERY_H hours
py voice.py --show            # the journal so far
```

## Why Robinhood Chain is the better half of this project

pump.fun's backend answers `401 Unauthorized` to an injected wallet, so its own
Create button can never complete a launch — the Solana repo has to bypass the
site entirely and mint through a signed transaction.

The pons launchpad **accepts the injected EIP-1193 wallet directly**. It
auto-connects with no modal, `eth_chainId` returns `0x1237`, `personal_sign`
round-trips. So here the site's own button is the real path — and on
2026-09-10 the amphood's click went all the way through it to a mined block.

## It launched

The amphood read the form through its retina and typed into it. The rig chose the
paired asset, opened **Advanced**, set the creator tax, clicked **Launch
token**, then clicked **Confirm** in the launchpad's own dialog. That click
produced exactly one `eth_sendTransaction`, which was signed in Python and
broadcast. Three of the launches, including the real one:

Every `status` `0x1`, every one 1,000,000,000 supply fixed at launch. The
test launches came from the first wallet; the real one, $amphoodBRAIN, from a
second wallet created for it. Its creator fees accrue as GOOGL and are shown
on 
— read them there rather than here, because they move. The first launch in full:

Read the receipt yourself rather than taking the table's word for it:


`from` is the amphood's wallet, `status` is `0x1`, and among the logs is a fresh
ERC-20 at `0x0` whose `name()` returns `test` and `symbol()` returns
`TEST`.

### The paired asset

pons pairs a new token against something already on Robinhood Chain, and what
is on Robinhood Chain is mostly tokenised equities — the menu is **57 assets**:
NVDA, SPCX, GOOGL, TSLA, GME, AAPL, SPY, and so on down to gold, oil and
Treasuries. The default is ETH. `set_pair_asset()` changes it, and the choice
is real: graduation goes from `4.2 ETH` to `24.2 GOOGL`.

The launch fee stays in ETH either way — the page says `GOOGL pair, ETH 0.0005
due` — so pairing against an equity needs none of that equity in the wallet.

```bash
amphood_PAIR=GOOGL amphood_TAX=2 py rhlive.py --port 4651
```

Two things about that menu are worth knowing if you automate it. It is a 262px
window onto a 2,064px list with **its own** scrollbar, so page scrolling cannot
reach inside it — `smooth_scroll_in()` eases the container's own `scrollTop`,
because `scrollIntoView` teleports and the list would cut from ETH to GOOGL
between two frames. And Playwright's `get_by_role("button", name="GOOGL")`
never resolves against it; the rows have to be found by `textContent` and
clicked at coordinates.

### Step 06: it learns now

`mushroom.py` is the one place in this project a weight is allowed to move,
and it moves where a amphood's weights actually move — the Kenyon cell to MBON
synapse, under dopamine.

The rule is the measured one. A Kenyon cell active shortly before a
dopaminergic neuron fires has **that synapse depressed**, not strengthened.
Learning in a amphood is subtraction: the mushroom body starts able to drive every
response and experience carves away the ones that did not pay. So there is no
potentiation here, only depression with a floor and a slow drift back toward
baseline standing in for forgetting.

Which MBONs count as reward-side and which as punishment-side is **not
hardcoded from a table**. For each MBON, total PAM input weight is compared
against total PPL1 input and the stronger wins. That split puts MBON01, 02 and
03 on the reward side and MBON04, 10 and 11 on the punishment side, which is
where the literature puts them — a good sign it is finding real structure
rather than noise.

```
44,042 KC->MBON synapses     27,939 reward-side     14,349 punish-side
```

Measured, with controls — twenty rewarded encounters with one view:

| population | change | expected |
|---|---|---|
| reward-side MBONs | **−6.0%** | depressed, it was the addressed compartment |
| punishment-side MBONs | −0.9% | ~0, never addressed |
| Kenyon cells | +0.3% | ~0, upstream of the synapse that changed |

**The reward signal is not real, and the module says so in as many words.** A
amphood is rewarded by sugar, not by reaching a web page. Novelty stands in for it
here, and that is a modelling choice made by a person — the amphood has no say in
it. The circuit, the plasticity site and the direction of the rule are the
parts that are real.

### Where it roams, and where it does not

The open web, plus the chain it launched its own token on: Wikipedia,
Wikimedia Commons, Wikisource, Hacker News, Project Gutenberg, Open Library,
xkcd, arXiv — and the pons launchpad, Blockscout, and the amphood's own token page.

Four places were tried and dropped, all for the same reason: a real browser
gets nothing usable from them.

| tried | what a headless browser actually gets |
|---|---|
| Google | 335 chars behind an "unusual traffic" wall |
| X | 623 chars of "Continue with phone" |
| old.reddit | blocked outright |
| archive.org | 0 chars — paints nothing headless, even at `networkidle` |

Open Library stands in for the Internet Archive, since it renders. The list is
what it is because a retina needs a page that exists, not because those sites
were uninteresting.

Keeping it on two domains was tried too, and the failure was quieter: 93 pages
and 110 clicks in 49 minutes across **6 unique pages**. It was moving the whole
time and going nowhere.

Trade controls are blocked and vetoed now that it roams a launchpad. It has no
wallet and a trade is impossible, but the claim was that every click is
checked, and it did once reach a "Buy token" page before that was tightened.

### Why there is no object store in the path

The public feed used to push a frame and a summary to a blob store twice a
second. That suspended the store on operation count — thirteen megabytes held,
every read answering `403` — and took the live feed down with it. Before that
it had a subtler problem: the CDN answered `X-Vercel-Cache: HIT` with an `Age`
of twenty seconds on a fixed pathname no matter what cache headers went with
the upload, because public blobs are treated as immutable.

So the amphood opens a cloudflared quick tunnel instead and the socket carries
frames, telemetry and events for free. The only thing published anywhere is
where the tunnel is — `site/web/live.json`, written when the address changes,
which the page reads. Quick tunnel addresses are random and change every run,
so nothing is hardcoded.


### Waiting for the chain, not for the click

A launch that had already succeeded looked exactly like a hang. The run loop
broke as soon as the page *asked* for a signature, so the rig declared itself
done about two seconds later — with the launchpad still showing "Confirming",
the recording cut, and the token appearing on-chain a few seconds after
everything had stopped.

The loop now waits for the receipt, on camera, and `send_transaction` takes
`wait_receipt=False` so the page gets its hash immediately: it is blocked on
that call and cannot render its own confirming state until the hash returns.

Then it ends where pump.fun would. pons does **not** redirect after a launch —
it leaves you on the empty create form — so `show_coin_page()` reads the token
address out of the receipt logs (the contract that answers `name()` and
`symbol()`), opens that token's page, accepts the terms gate that navigating
re-arms, and scrolls down it. The last thing on screen is the coin.

### The socials field

The X handle is `input[placeholder="handle"]`, `aria-label="X profile handle"`,
behind an `x.com/` prefix; Telegram sits next to it as `community`. Neither has
a name or an id, so the placeholder is the only stable handle on them. It is
typed like every other field and set by `amphood_RH_X`.

It is also optional on the form, and the rig treats it that way — a missing
field logs and the run continues rather than dying on a selector.

> The default is `elonmusk`, which is a **test value**. It has only ever been
> typed in dry runs. Putting a real person's handle on a live token presents
> that token as theirs, which is impersonation and gets both the token and the
> creator wallet flagged. Set `amphood_RH_X` to something you own before any live
> launch, or clear it.

### Dark mode was a flip, not a set

`go_dark()` clicks the site's theme *toggle*. That turned `/create` dark, and
then the coin page — which the site already remembered as dark — got flipped
back to **light** for the closing shot. It now measures the body background's
luma first and only flips when it has to, so the run both starts and ends dark.

### The bug that made the first attempt look like a success

The first live run reported a signed transaction and then nothing: the balance
never moved. `hexbytes >= 1.0` changed `.hex()` to return the raw hex *without*
the `0x` prefix, so `eth_sendRawTransaction` rejected the payload — and because
the failure came back through `page.expose_function`, the launchpad swallowed
it and the page just sat there. `send_transaction` now re-prefixes, logs a
rejection loudly, and polls for the receipt so a silent failure is not
possible.

## Check it yourself


**The wallet.** `py rhwallet.py new` generates a secp256k1 keypair, writes the
secret straight into gitignored `.env`, and prints only the address. It is never
printed, never returned, never passed through a chat window.

**The transaction path.** `py rhdryrun.py` exercises every step except the
broadcast: chain id, nonce, gas price, a real signed transaction, and — the
part that matters — recovering the signature and checking it against the
wallet's own address. Nothing is broadcast; there is no code path in that file
that can send.

```
chain id        4663 ok
nonce           0
gas price       0.1358 gwei
signed tx       110 bytes
recovered from  0x739Ccc9d…bFc3  MATCHES
estimateGas     21000 units
```

**The connectome.** CC-BY, from a public bucket, no account and no key:

```
https://storage.googleapis.com/amphoodem-male-cns/v1.0/connectome-data/
  body-annotations-male-cns-v1.0-minconf-0.5.feather      14 MB
  body-neurotransmitters-male-cns-v1.0.feather            42 MB
  connectome-weights-male-cns-v1.0-minconf-0.5.feather   1.1 GB
```

`py build_graph.py` turns those into 165,122 traced neurons and 10,228,000
signed edges. If your numbers differ from mine, one of us has a bug.

## What is NOT real, stated plainly

- **The amphood does not fill the whole form.** It reliably gets the description,
  often the ticker, rarely the name, and does not navigate to the launch button
  on its own. The rig completes whatever it misses, and the on-screen log says
  which fields were which — `by amphood: …  ·  by rig: …`.
- **Light mode breaks it.** The amphood's retina is a luminance map and every bit of
  tuning it has was done against dark UI. On the launchpad's default light theme
  it filled **0 of 3** fields; in dark mode, **2 of 3**. The rig switches the
  theme before it starts, and that gap is the clearest evidence its vision is
  doing real work.
- **The idle animation is decoration.** During a run every dot is a neuron at a
  measured soma coordinate. While idle it is a amphood-shaped scatter, and the panel
  label changes to say so.
- **The launch is one signature, and the rig arms it.** The launchpad asks for
  a single `eth_sendTransaction`; there is no second approval and no separate
  ERC-20 allowance. But the rig is what presses **Confirm** in the dialog, not
  the amphood — the amphood's contribution ends at the form and the launch button.
- **The amphood does not choose the paired asset.** It cannot read `GOOGL` at 892
  columns; picking a row out of a 57-item list is the rig following
  `amphood_RH_PAIR`. The same goes for the creator tax and the X handle.
- **The test tokens are tests.** `test (TEST)`, launched to prove the path
  end-to-end. It is not a project and nobody should buy it.
- **The voice is a narrator.** The amphood has no language. Every journal entry
  and every post on X is written by a language model handed the amphood's
  telemetry and the live numbers from its token page, and asked to write in
  the first person. Every number in a draft is checked against that packet;
  a draft with a number that is not in it, or with trading language, is
  thrown away. The neurons, the pages and the fees are real. The words, and
  any "confusion" or "curiosity" in them, are the narrator's.

## Running it

```bash
py rhwallet.py new              # create the wallet, then fund it (~0.002 ETH)
py rhdryrun.py                  # prove the signing path, spend nothing
py rhlive.py                    # http://localhost:4651, press START
py record.py --port 4651        # record the run to build/recordings/
```

A launch costs about **0.001 ETH** all in, so ~0.002 ETH in the wallet is
enough for a first one with room for the gas estimate to be wrong.

Two flags gate everything, both in `.env`, both off by default:

- `amphood_ALLOW_BROWSER=1` — required before a browser will open against a real
  site at all. A button in a web page is not a strong enough guard for that.
- `amphood_RH_LIVE=1` — required before any transaction is signed. Funding the
  wallet does not, on its own, arm anything.

## Fork it

```bash
python -m playwright install chromium

# the connectome itself - 1.1 GB, CC-BY, no account and no key
# (URLs under "Check it yourself" below), into data/
py build_graph.py            # -> build/graph.npz, 165,122 neurons

cp .env.example .env         # then set amphood_ALLOW_BROWSER=1
py roam.py                   # http://localhost:4660
```

MIT for the code. The connectome is **not ours to license** and stays CC-BY
wherever it goes — keep the attribution, it is the whole reason any of this is
real.

Things worth pointing it at that we have not:

- **A different readout.** The cursor comes out of DNa02, DNa01, MDN and DNp09
  because those are what a amphood walks with. Nothing says the output has to be a
  cursor.
- **The olfactory channel.** 2,635 ORNs across 53 receptor types are sitting
  there unused. cVA through ORN_DA1 drives pC1 at 222 Hz untrained, so the
  pathway works — it just has nothing plugged into it.
- **A real reward.** Ours is novelty, which is invented. Anything measurable
  and honest would be better.
- **Somewhere else entirely.** A game, a robot, a microscope. The brain does
  not know it is on a launchpad.

If you build something with it, open an issue — we would rather see it than
not.


## Hosting it

The roaming service runs as a single container. Build the graph first, so
`build/graph.npz` and `data/body-annotations.feather` exist, then:

```bash
docker build -t amphoodbrain .
docker run -p 4660:4660 amphoodbrain      # http://localhost:4660
```

To host it on Railway, run `railway up` from a checkout that has the graph
built; the data files are not in git, so a deploy straight from GitHub has
nothing to load. The service reads `PORT` and binds to every interface.

| variable | purpose |
|---|---|
| `PORT` | set by the host |
| `amphood_STATE_DIR` | where `mb_gains.npz` is kept; point it at a volume such as `/data` so learning survives redeploys |

The container has no wallet and no chain keys, and never signs anything.

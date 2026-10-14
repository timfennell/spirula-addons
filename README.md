# Spirula Studio add-ons

Two add-ons for [Spirula Studio](https://github.com/harry7557558/spirula-studio),
the Gaussian splat trainer, made while scanning pinned insects with a macro
camera rig. Each one installs on its own; pick one, or both.

| Add-on | What it does |
|---|---|
| [**Training animation capture**](training-capture/) | Records the model while it trains, from training views, an arc, or an orbit, as PNG sequences or H.264/H.265 video. |
| [**Insect voids**](insect-voids/) | Lets you draw voids inside a shiny body on cross sections of the model, so reflections can't be built as structure inside it, and the shell trains solid. |

![Training animation capture: an arc around a bee as it trains](media/training-capture-arc.gif)

*An arc capture of a bee training from scratch ([1080p video](media/training-capture-arc-1080p.mp4)).*

## Installing

**Easiest:** clone a ready-made branch of Spirula with the add-ons already in
it, from [timfennell/spirula-studio](https://github.com/timfennell/spirula-studio),
then build it as usual:

```bash
git clone -b insect-tools https://github.com/timfennell/spirula-studio      # both add-ons
git clone -b training-capture https://github.com/timfennell/spirula-studio  # capture only
git clone -b insect-voids https://github.com/timfennell/spirula-studio      # voids only
```

**Or patch your own clone.** The add-ons are also plain source patches you
can apply to a clone of Spirula Studio. They're made against upstream `master` at
[`d6d0d855`](https://github.com/harry7557558/spirula-studio/commit/d6d0d855)
(2026-10-14).

```bash
git clone https://github.com/harry7557558/spirula-studio
cd spirula-studio
git checkout -b addons d6d0d855
```

Then apply **one** of these:

```bash
# Training animation capture only
curl -L https://raw.githubusercontent.com/timfennell/spirula-addons/main/training-capture/training-capture.patch | git am

# Insect voids only
curl -L https://raw.githubusercontent.com/timfennell/spirula-addons/main/insect-voids/insect-voids.patch | git am

# Both
curl -L https://raw.githubusercontent.com/timfennell/spirula-addons/main/both/insect-tools-both.patch | git am
```

Use the **Both** patch if you want both add-ons. The two single patches touch
the same few lines of the trainer screen, so they don't stack on each other.

Then build Spirula as its [build guide](https://github.com/harry7557558/spirula-studio/blob/master/docs/build.md)
describes. On macOS that's:

```bash
./build_develop.bash -DSS_BACKEND=vulkan
```

**Newer versions of Spirula:** the patches usually still apply. Use
`git am -3` so small changes are merged for you. If a patch stops applying,
please open an issue.

## Tested on

macOS 26 on an Apple M2 Pro (16 GB), Vulkan backend via MoltenVK. Most of
both add-ons is backend-neutral. *Voids block light* (part of Insect voids)
is Vulkan only; on CUDA builds it switches itself off and says so in the log.

## License

GPL-3.0, the same as Spirula Studio.

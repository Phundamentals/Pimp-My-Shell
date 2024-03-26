# Oh-My-Posh

### Todo

- [ ] Json vs Yaml vs Toml
- [ ] Can themes be [extended](https://ohmyposh.dev/docs/configuration/secondary-prompt#configuration)?
  _I don't think so, probably a wording issue_.
- [ ] Color templates.
- [ ] Sprig.
- [ ] Derive from built-in defaults to stay up-to-date.

### Concepts

- **Block**: a container for segments that define position, alignment, overflow and more.  
  A block can be left-aligned (`prompt`) or right-aligned (`rprompt`).
- **Segment**: a unit with informational context: it has a _subject_.
  - **Plain**: colored text on a transparent background.
  - **Powerline**: a powerline has one symbol and takes the background of the previous segment and the foreground of the
    current segment.
  - **Diamond**: like a powerline with a starting and an ending symbol with the segment's background as the foreground.
  - **Accordion**: like a powerline, displays even when disabled but shows no text when disabled.

A _segment_:

- can have properties such as `include_folders []` and `exclude_folders []` to render it only in certain folders.
- the arguments are regular expressions and must match the full directory name.
- accepts both `/` and `\` as directory separators.
- needs a `\` to be escaped as `\\\\` in the regular expression.
- a `~` at the start will match the user's home directory.
- compares case-insensitive on Windows, case-sensitive otherwise.
- will be hidden if it is empty or contains only spaces.

### Structure

```json
{
  "$schema": "https://raw.githubusercontent.com/JanDeDobbeleer/oh-my-posh/main/themes/schema.json",
  "blocks": [
    {
      "type": "prompt",
      "alignment": "left",
      "segments": [
      ]
    },
    {
      "type": "rprompt",
      "segments": [
      ]
    }
  ],
  "final_space": true,
  "version": 2
}
```

### Colors

A color can be specified as:

- An HTML hexadecimal value.
- One of the 16 ANSI color names:  
  `black` `red` `green` `yellow` `blue` `magenta` `cyan` `white` `default`  
  `darkGray` `lightRed` `lightGreen` `lightYellow` `lightBlue` `lightMagenta` `lightCyan` `lightWhite`
- A 256 color palette using numbers (_reference?_).
- One of the keywords:  
  `transparent` `foreground` `background` `parentForeground` `parentBackground`  
  `accent` (OS accent color, Windows only).

Colors can be overriden by using the syntax `<foreground,background>text</>` or `<,background>text</>`.

A palette of standard colors can be defined with `"palette": {}`. These colors can than be referenced as
`"foreground": "p:palette-key"`. Invalid keys will be resolved as `transparent`.

Palette entries can contain recursive references to other palette entries: You can define a named set of standard
colors, and have segment-specific names reference them.

The palettes entry can activate one of multiple palettes
[conditionally](https://ohmyposh.dev/docs/configuration/colors#palettes) by using its `template` property.

Palette colors can be [cycled](https://ohmyposh.dev/docs/configuration/colors#cycle).

### Templates

Templates use [Go's text templating](https://pkg.go.dev/text/template) extended with
[Sprig](https://masterminds.github.io/sprig/). Refer to [the manual](https://ohmyposh.dev/docs/configuration/templates)
for more information.

_If a segment overrides a global property, prefix it with `$` to reference the global property instead_.

Templates can contain HTML-like syntax for: bold `b`, italic `i`, underline `u`, overline `o`, strikethrough `s`, dimmed
`d`, blink `f`, reversed `r`.

### Prompts

- Primary.
- Secondary: continuation.
- Debug: only with Powershell.
- Transient: limited support, Bash is excluded.
- Tooltips: limited support.

### Opinionated list of most interesting segment types

- [Battery](https://ohmyposh.dev/docs/segments/battery)
- [Command](https://ohmyposh.dev/docs/segments/command)
- [DotNet](https://ohmyposh.dev/docs/segments/dotnet)
- [Execution Time](https://ohmyposh.dev/docs/segments/executiontime)
- [Git](https://ohmyposh.dev/docs/segments/git)
- [GitVersion](https://ohmyposh.dev/docs/segments/gitversion)
- [Node](https://ohmyposh.dev/docs/segments/node)
- [NPM](https://ohmyposh.dev/docs/segments/npm)
- [OS](https://ohmyposh.dev/docs/segments/os)
- [Path](https://ohmyposh.dev/docs/segments/path)
- [Project](https://ohmyposh.dev/docs/segments/project)
- [Root](https://ohmyposh.dev/docs/segments/root)
- [Session](https://ohmyposh.dev/docs/segments/session)
- [Shell](https://ohmyposh.dev/docs/segments/shell)
- [Status Code](https://ohmyposh.dev/docs/segments/status)
- [System Info](https://ohmyposh.dev/docs/segments/sysinfo)
- [Text](https://ohmyposh.dev/docs/segments/text)
- [Time](https://ohmyposh.dev/docs/segments/time)
- [Upgrade](https://ohmyposh.dev/docs/segments/upgrade)

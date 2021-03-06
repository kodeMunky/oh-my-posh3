---
id: upgrading
title: Upgrading
sidebar_label: 🤘 Upgrading from V2
---

Just like V2, V3 is available in the [PowerShell gallery][psgallery]. Due to its nature, it's only
available as a prerelease while we work out the kinks and get it on par with V2.

## V2's problem statement

V2 has Powershell module files as [themes][themesv2]. That way of working was inspired from [oh-my-zsh][omz] and other
prompt rendering tools, but that approach has a few important downsides.

- hard to extend/adjust when you're not proficient
- the need to expose a lot of functions/settings to allow ease of personalization
- limited to Powershell

## Enter V3

This bring us to the first change, to allow a cross platform experience, [Oh My Posh V3][v3] is written entirely in [Go][golang].
That way, cross platform binaries can be shipped which render the same prompt using the same config anywhere.

The configuration is changed from `$ThemeSettings` towards a `.json` file that only contains the configuration for the
blocks and segments you want to render. See [concept][introduction] for more context on that part.

Let's have a look at the V2 commands and how to move towards V3.

## Import

Stays the same! Alright. All you need to do is update to the **beta**.

```powershell
Update-Module -Name oh-my-posh -AllowPrerelease -Scope CurrentUser
```

## Configuration

Here we have a few options. If you're using an out-of-the box theme, you can simply change the current command to the
new one, provided your V2 theme has already been added to [V3][themesv3].

### I use an out-of-the-box theme

Change the current prompt setting function to the new one.

```powershell
# Set-Theme Agnoster
Set-PoshPrompt -Theme agnoster
```

### I use a custom theme/settings

The first thing to do is to look for the theme you based your theme on.
If you don't remember which one, preview them all and take the one closest to yours.

```powershell
Get-PoshThemes
```

If you see one you like, set it, export its config so you can customize/extend the blocks ans segmnts.

```powershell
Set-PoshPrompt -Theme jandedobbeleer
Write-PoshTheme | Out-File -FilePath ~/.go-my-posh.json
```

Adjust the config (`~/.go-my-posh.json`) to your liking by going through the [configuration][configuration] guide.
Set your custom theme and enjoy.

```powershell
Set-PoshPrompt -Theme  ~/.go-my-posh.json
```

### I have no idea just yet

Great! There's an option for that too. You can easily list all available themes and pick the one you like best.

```powershell
Get-PoshThemes
```

Choose and set the one you like.

```powershell
Set-PoshPrompt -Theme jandedobbeleer
```

## All set, now what

You can either tweak the theme to your liking, add segments or [submit an issue][issues] for new functionality.
Do not hesitate to [ask for assistance][issues] when you notice an issue or unexpected behavior.

[manual]: /docs/installation
[psgallery]: https://www.powershellgallery.com/packages/oh-my-posh
[themesv2]: https://github.com/JanDeDobbeleer/oh-my-posh/tree/master/Themes
[omz]: https://github.com/ohmyzsh/ohmyzsh
[golang]: https://golang.org/
[introduction]: /docs/#concept
[v3]: https://github.com/JanDeDobbeleer/oh-my-posh3/
[themesv3]: https://github.com/JanDeDobbeleer/oh-my-posh3/tree/main/themes
[configuration]: /docs/configure
[issues]: https://github.com/JanDeDobbeleer/oh-my-posh3/issues/new

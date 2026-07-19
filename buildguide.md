# macOS Build Guide

## Foundation

1. Enable Dark Mode 
1. Mac App Store
	- Bitwarden: https://apps.apple.com/us/app/bitwarden/id1352778147?mt=12
		- Enable SSH agent in settings
		- Set to run at startup
		- Enable biometrics in Firefox & Brave
	- Yubico Authenticator: https://apps.apple.com/us/app/yubico-authenticator/id1497506650?mt=12
1. Log into Bitwarden
1. Install [Homebrew](https://brew.sh/)
	1. Set up Auto-Update

		```bash
		brew install pinentry-mac
		brew tap domt4/autoupdate
		brew autoupdate start 43200 --upgrade --cleanup --immediate --sudo
		```

	1. Install Bitwarden CLI

```bash
		brew install bitwarden-cli
```

1. Install & set up MEGAsync

```bash
brew install megasync
```

1. Install Obsidian via brew, or manually if you don't have admin

```bash
brew install obsidian
```

## Obsidian Setup

1. Sync Main vault to ~/obsidian
1. Set up backup in MEGA

## Installs

### App Store Installs

- Windows App: https://apps.apple.com/us/app/windows-app/id1295203466?mt=12
- The Unarchiver: https://apps.apple.com/us/app/the-unarchiver/id425424353?mt=12
- Slack: https://apps.apple.com/us/app/slack-for-desktop/id803453959?mt=12
- Clocker: https://apps.apple.com/us/app/clocker/id1056643111?mt=12
- Amphetamine: https://apps.apple.com/us/app/amphetamine/id937984704?mt=12
- Wireguard: https://apps.apple.com/us/app/wireguard/id1451685025?mt=12
- Paprika: https://apps.apple.com/us/app/paprika-recipe-manager-3/id1303222628?mt=12
- Microsoft 365: https://apps.apple.com/us/app-bundle/microsoft-365/id1450038993?mt=12
- Poolsuite FM: https://apps.apple.com/us/app/poolsuite-fm/id1514817810
- Kindle: https://apps.apple.com/us/app/amazon-kindle/id302584613

### Homebrew Installs

```bash
brew install nano
brew install starship
brew install mise
brew install git
brew install curl
brew install chezmoi
brew install font-cascadia-mono-nf
brew install git-credential-manager
brew install firefox
brew install firefoxpwa
brew install brave-browser
brew install powershell/tap/powershell
brew install zsh-syntax-highlighting
brew install tabby
brew install stats
brew install alt-tab
brew install discord
brew install cyberduck
brew install calibre
brew install gimp
brew install send-to-kindle
brew install steam
brew install visual-studio-code
brew install vlc
brew install vscodium
brew install balenaetcher
brew install sheldon
brew install podman
brew install podman-compose
brew install podman-desktop
```

### Manual Installs

- VMware Fusion: https://blogs.vmware.com/teamfusion/2024/05/fusion-pro-now-available-free-for-personal-use.html

## Configuration

### Settings App

1. Apple Account
	1. Sign in
1. Bluetooth
	1. Pair devices
1. General
	1. Date & Time
		1. `Set time zone automatically using your current location` to `on`
	1. Language & region
		1. `Live Text` to `on`
1. Appearance
	1. `Appearance` to `Dark`
1. Control Center
	1. Control Center Modules
		1. `Wi-Fi` to `Show`
		1. `Bluetooth` to `Don't Show`
		1. `AirDrop` to `Don't Show`
		1. `Focus` to `Show when Active`
		1. `Stage Manager` to `Don't Show`
		1. `Screen Mirroring` to `Show when Active`
		1. `Display` to `Show when Active`
		1. `Sound` to `Always Show`
	1. Battery
		1. `Show in Menu Bar` to `off`
		1. `Show in Control Center` to `on`
		1. `Show Percentage` to `on`
	1. Menu Bar Only
		1. Clock > Clock Options
			1. `Style` to `Analog` (skip if you aren't planning to use Clocker)
		1. `Spotlight` to `Don't Show`
		1. `Siri` to `Don't Show`
		1. `Time Machine` to `Don't Show`
		1. `Weather` to `Don't Show`
	1. `Automatically hide and show the menu bar` to `In Full Screen Only`
1. Desktop & Dock
	1. Adjust `Size` and `Magnification` as you wish
	1. `Minimize windows using` to `Genie Effect`
	1. `Minimize windows into application icon` to `on`
	1. `Automatically hide and show the Dock` to `off`
	1. `Animate opening applications` to `on`
	1. `Show indicators for open application` to `on`
	1. `Show suggested and recent apps in Dock` to `off`
	1. `Default web browser` to `Firefox`
	1. `Drag windows to screen edges to tile` to `on`
	1. `Drag windows to menu bar to fill screen` to `on`
	1. `Hold Opt key while dragging windows to tile` to `off`
	1. `Tiled windows have margins` to `off`
1. Touch ID & Password
	1. Set up Touch ID
1. Printers & Scanners
	1. Add printer

### Other

1. Associate .ics files with Outlook
1. Enable Touch ID for sudo

    ```shell
    sed "s/^#auth/auth/" /etc/pam.d/sudo_local.template | sudo tee /etc/pam.d/sudo_local
    ```

## Chezmoi

```
chezmoi init natescherer
```

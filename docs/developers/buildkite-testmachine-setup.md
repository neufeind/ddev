<h1>Buildkite Test Agent Setup</h1>

We are using [Buildkite](https://buildkite.com/drud) for Windows and macOS testing. The build machines and buildkite-agent must be set up before use.

## Windows Test Agent Setup:

1. Install [chocolatey](https://chocolatey.org/)
2. Install golang/make/git/docker-ce/nssm with `choco install -y golang make git docker-for-windows mariadb nssm`
3. If a laptop, set the "lid closing" setting in settings to do nothing.
4. Set the "Sleep after time" setting in settings to never.
5. Install the buildkite-agent. Use the latest release from [github.com/buildkite/agent](https://github.com/buildkite/agent/releases). It should go in /c/buildkite-agent, with the buildkite-agent.exe in /c/buildkite-agent/bin and the config in /c/buildkite-agent.
6. Update the buildkite-agent.cfg with the token and tags. Tags will probably be like `"os=windows,osvariant=windows10pro,dockertype=dockerforwindows"` or `"os=windows,osvariant=windows10pro,dockertype=toolbox"`.
7. Set up the agent to [run as a service](https://buildkite.com/docs/agent/v3/windows#running-as-a-service), preferably as the primary user of the machine, so it inherits environment variables and such. It must be set up to log in as the user.
8. Set up the machine to [automatically log in on boot](https://www.cnet.com/how-to/automatically-log-in-to-your-windows-10-pc/).  Run netplwiz, provide the password for the main user, uncheck the "require a password to log in".
9. On Docker Toolbox systems, add a link to "Docker Quickstart Terminal" in C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp (see [link](http://www.thewindowsclub.com/make-programs-run-on-startup-windows)).
10. Reboot the machine and do a test run.

### macOS Test Agent Setup

1. Install [homebrew](https://brew.sh/)
2. Install golang/git/docker with `brew install golang git buildkite-agent mysql`
3. Install docker with `brew cask install docker`
4. If the xcode command line tools are not yet installed, install them with `xcode select --install`
5. Edit the buildkite-agent.cfg in /usr/local/etc/buildkite-agent.cfg to add the agent token and the tags. Tags will probably be like `"os=macos,osvariant=highsierra,dockertype=dockerformac"`
6. Install nosleep `brew cask install nosleep`
7. Enable nosleep using its shortcut in the Mac status bar.
8. In nosleep Preferences, enable "Never sleep on AC Adapter", "Never sleep on Battery", and "Start nosleep utility on system startup".
9. Set up Mac to [automatically log in on boot](https://support.apple.com/en-us/HT201476).
10. Reboot the machine and do a test run.

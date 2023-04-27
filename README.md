# Jetson Dev Container Template

Jetson内でVSCodeのDevContainerを使って開発するときのテンプレ

## Setup SSH

Remote SSHで作業できるように `~/.ssh/config` を設定する

```~/.ssh/config
Host orin-nano
	HostName orin-nano.local
	User <username>
	StrictHostKeyChecking no
	UserKnownHostsFile=/dev/null
	ForwardAgent yes
	ForwardX11 yes
	ForwardX11Trusted yes
```

鍵でログイン可能にする

```sh
ssh-copy-id orin-nano
```

### Setup X11

#### Local Machine

Ubuntuを想定している。

```diff: ~/.bashrc
+ export DISPLAY=localhost:0.0
```

リモートでつないでGUIなアプリケーションが実行できたらOK

```sh
xeyes
```

## Run with Docker

使いたいディレクトリに `.devcontainer` のディレクトリを配置して
`Ctrl+P` -> `Dev Containers: Reopen in Container` で開く

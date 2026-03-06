# Infrastructure

## 小龙虾 (EC2)
- Type: t3.medium (i-0a429584531e086a8)
- Region: us-west-2, Ubuntu 24.04
- IP: 35.94.57.103
- Key: test20260204, SG: corp
- SSH: `ssh -i ~/.ssh/test20260204.pem ubuntu@35.94.57.103`
- Systemd: openclaw.service (enabled)
- 迁移完成 2/24-25

## 天蝎 (EC2)
- Region: us-west-2
- 已从 c6i.8xlarge 降级（Ronnie 2/25 手动完成，省 ~$950/月）

## Git 备份
- Repo: git@github.com:yugiohdark/xiaolongxia-backup.git
- Deploy key: ~/.ssh/id_ed25519

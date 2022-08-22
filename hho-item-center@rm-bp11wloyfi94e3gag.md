



一级类目（服装服饰、 352484011     颜色、大小 已加

时尚):   2229202051  颜色、大小.  [{"key":"item_attr_color_option"},{"key":"item_attr_size_option"}]



家电、摄影、视频音频  /  电子配件及用品 / 手机配件/  手机保护壳（3210981-128187011-128189011-128199011）

[{"key":"item_attr_device_model_option"},{"key":"item_attr_color_option"}]



```mysql
/* 请确认以下SQL符合您的变更需求，务必确认无误后再提交执行 */

CREATE TABLE `item_competitor_image` (
	`id` bigint(20) NOT NULL AUTO_INCREMENT COMMENT '主键',
	`item_id` varchar(20) CHARACTER SET utf8 COLLATE utf8_general_ci NULL COMMENT '原商品ID',
	`item_image` varchar(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL COMMENT '原商品图片链接',
	`competitor_image` varchar(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL COMMENT '竞品图片链接',
	`title` text CHARACTER SET utf8 COLLATE utf8_general_ci NULL COMMENT '竞品标题',
	`rating` varchar(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL COMMENT '竞品评分',
	`rating_number` varchar(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL COMMENT '竞品评分数',
	`link` text CHARACTER SET utf8 COLLATE utf8_general_ci NULL COMMENT '竞品链接',
	`price` varchar(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL COMMENT '竞品价格',
	`dup_score` decimal(20,4)  NULL COMMENT '图片相似度',
	PRIMARY KEY (`id`)
) ENGINE=InnoDB
DEFAULT CHARACTER SET=utf8 COLLATE=utf8_general_ci
COMMENT='商品的相关竞品信息表'
AUTO_INCREMENT=57
ROW_FORMAT=DYNAMIC
AVG_ROW_LENGTH=0;


```








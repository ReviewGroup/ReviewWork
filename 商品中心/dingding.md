

org.springframework.context.ApplicationContextException: Failed to start bean 'documentationPluginsBootstrapper'; nested exception is 
java.lang.NullPointerException
        at org.springframework.context.support.DefaultLifecycleProcessor.doStart(DefaultLifecycleProcessor.java:181)
        at org.springframework.context.support.DefaultLifecycleProcessor.access$200(DefaultLifecycleProcessor.java:54)
        at org.springframework.context.support.DefaultLifecycleProcessor$LifecycleGroup.start(DefaultLifecycleProcessor.java:356)
        at java.base/java.lang.Iterable.forEach(Iterable.java:75)
        at org.springframework.context.support.DefaultLifecycleProcessor.startBeans(DefaultLifecycleProcessor.java:155)
        at org.springframework.context.support.DefaultLifecycleProcessor.onRefresh(DefaultLifecycleProcessor.java:123)
        at org.springframework.context.support.AbstractApplicationContext.finishRefresh(AbstractApplicationContext.java:935)
        at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:586)
        at org.springframework.boot.web.servlet.context.ServletWebServerApplicationContext.refresh(ServletWebServerApplicationContext.
java:147)
        at org.springframework.boot.SpringApplication.refresh(SpringApplication.java:734)
        at org.springframework.boot.SpringApplication.refreshContext(SpringApplication.java:408)
        at org.springframework.boot.SpringApplication.run(SpringApplication.java:308)
        at org.springframework.boot.SpringApplication.run(SpringApplication.java:1306)
        at org.springframework.boot.SpringApplication.run(SpringApplication.java:1295)
        at com.hho.item.center.Application.main(Application.java:21)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.base/java.lang.reflect.Method.invoke(Method.java:566)
        at org.springframework.boot.loader.MainMethodRunner.run(MainMethodRunner.java:49)
        at org.springframework.boot.loader.Launcher.launch(Launcher.java:107)
        at org.springframework.boot.loader.Launcher.launch(Launcher.java:58)
        at org.springframework.boot.loader.JarLauncher.main(JarLauncher.java:88)
Caused by: java.lang.NullPointerException: null
        at springfox.documentation.spi.service.contexts.Orderings$8.compare(Orderings.java:113)
        at springfox.documentation.spi.service.contexts.Orderings$8.compare(Orderings.java:110)



  •  case2：看看不符合优价&毛利率存量商品，已有日本用户应援过 Action：流量降权，不让其他用户看到了。——8.5完成
1.流量降权如何做？ 将要降权的商品告诉C端吗？
——是的，需要feeds在展现策略上对后台输出的商品list做处理。@红洋

这个还没做吧？



  •  case3：应援成功的已上架预售商品，预售价格＞应援价格（当前紧急）   Action：手动替换竞品链接（已更新80+，剩余200款），按照【优价&商业成立】原则调价，符合原则的完成价格更新，并通知用户发送优惠券。不符合原则，下架。——8.10



  1  手动替换是做什么？ 改成价格低的竞品链接还是更高的？是发任务通知让店铺改？
——发任务给店铺做，手动替换更合理的竞品，不是强制更高或者更低，是功能上可以对标的竞品。竞品更新后，价格符合就更新价格重新上架，价格不符合上架要求就不再上架。

  2  【优价&商业成立】原则是什么？ 价格更新是重新价格审批吗？发钉钉消息通知调价吗
——原则是后台是否能通过系统审核。重新定价就是重新发起价格审批。

  3  发优惠券是如何发的？找C端提供接口？需要通知吗：客户端通知？ 邮件通知？
——发优惠券，你负责把需要发优惠券的商品和用户列表输出，发放优惠券需要和@李明联动来做。邮件通知，需要@瑞穗确认名单和邮件内容后系统来执行发送。

临时需求： 生成 需要发优惠券。输出  优惠券的价格？



  •  case4：应援成功的已上架预售商品，预售价格＜应援价格，不符合优价&毛利率 Action：手动更新竞品链接，商品上架7天后执行【优价&商业成立】原则，调价。不符合原则的，下架。——8.13完成
  1  商品上架7天后执行，调价，是钉钉通知让店铺调价吗，不符合原则的商品下架前有多久的处理时间？
——设计策略是先通知，店铺72小时内执行。

  •  货源自动巡检 Action：第一轮全量巡检8.5完成，自动每天自动巡检，进入异常列表+商品状态标记。



应援上架时间早于7月20日，预售上架7天以内，预售价格必须＜应援价格，接受毛利率为负

应援上架时间晚于7月20日，预售价格必须＜应援价格，不接受毛利率为负





task 

1.    可配置 超时自动下架时间  。 system get set方法 
2.   前端时间展示。 系统用户 星星 TODO



3.  价格变化巡检





0803_fix spring 升级



```
"预售价高于应援价格", "此商品预售价高于应援价格，请替换更合理的竞品并重新发起价格审批，若价格不能通过审批将下架商品",
"选品源下架", "请替换同品货源或者下架商品，处理后需要手动完成",        需要手动完成状态
"售价高于竞品价格9折", "请确认竞品链接后，重新发起价格审批。若价格不能通过审批将下架商品"
"货源价格变化", "请确认竞品链接后，重新发起价格审批。若价格不能通过审批将下架商品"   需要手动完成状态
"负毛利率商品", "请确认竞品链接后，重新发起价格审批。若价格不能通过审批将下架商品"
"缺失实拍图片/实拍视频", "此商品缺失实拍图片/实拍视频，请添加图片或视频"
```

审批流 azhu 

超时任务

配置

优先级



```
策略：
1. 任务剩余时间提醒
2. 待处理的异常任务超过规定时间后，发起商品下架的审批流程
   2.1 （待定）审批流程：
   发起审批 -》给商品的店长批准-》 
   若同意则下架商品，关闭任务，结束审批 
   若不同意填写理由发给易统审核
   -》易统同意下架则直接下架商品
   不同意下架则关闭任务
   审批若没人处理怎么办：自动下架
   
   2.2 （待确定）任务优先级排序和超时时间：
    优先级：紧急：12h>重要24h> 一般72h
    选品源下架：紧急；
    预售价高于应援价格/售价高于竞品价格9折：重要
    负毛利率商品/货源价格变化导致的负毛利：一般
    
3. 每天生成异常任务未处理而下架的列表，发送给店铺负责人
   钉钉发送excel文件（待定）   
    
目标：紧急/重要异常任务100%清除
```

/* 请确认以下SQL符合您的变更需求，务必确认无误后再提交执行 */

ALTER TABLE `assign_task` 
	CHANGE COLUMN `work_flow_id` `workflow_id` varchar(30) CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci NULL COMMENT '工作流ID' AFTER `context`
;

# ABtest

## 1. ABtest组件

![](<../../.gitbook/assets/image (285).png>)

1. 新增ABtest组件，在「起始组件」、「用户判断」、「事件触发」、「活动配置」四个组件后，均可设置ABtest组件
2. 在ABtest组件的分支当中，不可再添加ABtest组件



## 2. 添加ABtest组件

![](<../../.gitbook/assets/image (287).png>)

1. 添加ABtest组件后，进入到配置页面
2. 首先设置ABtest的衡量目标，支持”在xx久之内，完成xx事件“的配置规则。当实际上线运行后，每一个分流到某个分支的用户，会自动从其流入到该分支时刻开始计时，最终判定是否满足”在xx久之内，完成xx事件“的目标。以此作为目标完成率的计算依据，判定不同分支策略的有效性
3. 最多支持1个对照组，9个实验组，各分支比例可灵活配置

## 3. 分支策略配置

![ ](<../../.gitbook/assets/image (284).png>)

1. 当ABtest组件配置完成后，会根据设置的分支数，自动生成如上图所示的分支流程
2. 其中每个分支均可用「用户判断器」、「事件触发器」、「活动配置」三个组件灵活配置复杂的策略流
3. ABtest每个分支当中，不支持再添加abtest组件，但一个流程画布内可支持多个abtest组件



## 4. 数据统计

![](<../../.gitbook/assets/image (286).png>)

1. 在画布详情页中，ABtest组件有详细的分支数据统计，包括各分支流入人次、ABtest目标完成率
2. 各分支中的策略，均有每一步流转的统计数据，包括人次流向、活动完成率漏斗

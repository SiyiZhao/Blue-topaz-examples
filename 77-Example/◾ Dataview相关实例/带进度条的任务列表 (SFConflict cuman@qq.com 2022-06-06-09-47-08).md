---
Title: 任务情况
Total: 6
Incomplete: 2
Completed: 4
cssclass: tasks
tag: 任务进度
updated: 2022-04-06 10:02
---
## 带进度条的任务列表
> 会自动统计当前文档任务总数和已完成的任务数量。
需要配合metaedit插件完成 yaml 区域数据的自动更新。

- `="<progress  class='green' value=" + this.Completed +" max="+ this.Total+"></progress> "+this.Completed+"/"+ this.Total`
-  百分比任务条通过dv插件动态实时更新
- `$= const value = ((dv.current().file.tasks.where(t => t.completed).length) / (dv.current().file.tasks).length || 0) * 100; "<progress value='" + value + "' max='100'></progress>" + " " + value.toFixed(2) + "%"`
	- [x] 第一个任务
	- [x] 第二个任务 ✅ 2022-06-06
	- [x] 第三个任务 ✅ 2022-05-29
		- [ ] 第三个子任务
		- [ ] 第三个子任务2
	- [x] 第四个任务

## 任务列表汇总

> 会把所有含`#任务进度`标签的文档汇总起来，方便查看文档中的任务完成情况。
需要配合metaedit插件完成 yaml 区域数据的自动更新。

### 样式1

```dataviewjs
function projectTracker(dv,query){
let searchPagePaths = dv.pages(query).file.path
for(let i=0; i < searchPagePaths.length; i++){
if(dv.page(searchPagePaths[i]).Total){
let title = dv.page(searchPagePaths[i]).Title;
let total = dv.page(searchPagePaths[i]).Total;
let completed = dv.page(searchPagePaths[i]).Completed;
let status =
((dv.page(searchPagePaths[i]).Completed /
dv.page(searchPagePaths[i]).Total) * 100).toFixed();
let link =dv.page(searchPagePaths[i]).file.link;
const progress = "<progress class='green' value=" + completed +" max="+ total +"></progress> "+completed+"/"+ total;
dv.paragraph(link);
dv.paragraph(progress);
}
}
}
projectTracker(
dv,
"#任务进度"
)
```

### 样式2


```dataviewjs
function projectTracker(dv,query){
let searchPagePaths = dv.pages(query).file.path
for(let i=0; i < searchPagePaths.length; i++){
if(dv.page(searchPagePaths[i]).Total){
let title = dv.page(searchPagePaths[i]).Title;
let total = dv.page(searchPagePaths[i]).Total;
let status =
((dv.page(searchPagePaths[i]).Completed /
dv.page(searchPagePaths[i]).Total) * 100).toFixed();
let link =dv.page(searchPagePaths[i]).file.link;
const progress = "![](https://progress-bar.dev/" + status + "/?scale=" + "100" + "&title=" + title + "&width=300)";
dv.paragraph(link);
dv.paragraph(progress);
}
}
}
projectTracker(
dv,
"#任务进度"
)
```










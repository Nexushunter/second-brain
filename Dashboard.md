## Quick Links
- list of links that you find valuable.

## Mental Health 💚
```dataviewjs
let mood = ["#greatDay", "#goodDay", "#okayDay", "#badDay", "#terribleDay"]
let tagLists = dv.pages('"DailyJournal"').map(p => p.file.tags.filter(tag => mood.contains(tag)));
let tags = [...tagLists.filter(tagList => tagList.length > 0)].reduce((cumu, curr) => cumu.concat(curr));
let data = [
	tags.filter(tag => tag == mood[0]).length,
	tags.filter(tag => tag == mood[1]).length,
	tags.filter(tag => tag == mood[2]).length,
	tags.filter(tag => tag == mood[3]).length,
	tags.filter(tag => tag == mood[4]).length
];

const chartData = {  
	type: 'pie',  
	data: {  
		labels: mood,  
		datasets: [{  
			label: 'Mark',  
			data: data,  
			backgroundColor: [
			'rgba(43, 227, 62, 0.2)',// green
			'rgba(41, 159, 255, 0.2)', // blue
			'rgba(176, 92, 250, 0.2)', // purple
			'rgba(255, 148, 48, 0.2)', // orange
			'rgba(235, 64, 52, 0.2)' // red
			],  
			borderColor: ['rgba(255, 99, 132, 1)'],
			borderWidth: 1,
		}]  
	}  
}  
window.renderChart(chartData, this.container)
```


## Daily Task Productivity
```dataviewjs
let totalTaskCount = [];
let completedTaskCount = [];
let taskDates = [];
let pages = dv.pages('"DailyJournal"').values;

for (var i = 0; i < pages.length; i++) {
	let page = pages[i];
	let allTasks = page.file.tasks;
	let workTasks = allTasks.filter(taskList => taskList.section.subpath == "Work Tasks");
	let completedTasks = workTasks.filter(tasks => tasks.completed);
	totalTaskCount.push(workTasks.length);
	completedTaskCount.push(completedTasks.length);
	taskDates.push(page.name);
}

let days = Array.from({length: totalTaskCount.length}, (v, k) => k+1);
var trace1 = {
	x: days,
	y: totalTaskCount,
	name: 'Total Tasks To Complete',
	marker: {color: 'rgb(55, 83, 109)'},
	fill: 'tonexty',
	type: 'scatter'
};

var trace2 = {
	x: days,
	y: completedTaskCount,
	name: 'Tasks Completed',
	marker: {color: 'rgb(45, 237, 61)'},
	fill: 'tozeroy',
	type: 'scatter'
};

var data = [trace1, trace2];
var layout = {
	title: 'Daily Task Completions',
	xaxis: {
		tickfont: {
			size: 14,
			color: 'rgb(107, 107, 107)'
		}
	},
	yaxis: {
		title: 'Number of Tasks',
		titlefont: {
			size: 16,
			color: 'rgb(107, 107, 107)'
		},
		tickfont: {
			size: 14,
			color: 'rgb(107, 107, 107)'
		}
	},
	legend: {
		x: 0,
		y: 1.0,
		bgcolor: 'rgba(255, 255, 255, 0)',
		bordercolor: 'rgba(255, 255, 255, 0)'
	},
	barmode: 'group',
	bargap: 0.15,
	bargroupgap: 0.1
};
var config = {
	displaylogo:false,
	responsive: true
};

window.renderPlotly(this.container, data, layout, config)
```


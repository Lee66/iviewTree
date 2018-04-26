<template>
	<div id="app">
		<Tree class="menu" :data="data1" @on-select-change="getUser" children-key="group"></Tree>
		<div class="right">
			<Input v-model="value" placeholder="请输入筛选的名字" style="width: 300px"></Input>
			<i-table class="table" :columns="columns1" :data="tabData"></i-table>
		</div>
	</div>
</template>
<script>
	let tree = [{
			"title": "总部门",
			"expand": false,
			"selected": true,
			"user": [{
					"name": "Prometheus",
					"sex": "male"
				},
				{
					"name": "Athena",
					"sex": "female"
				},
				{
					"name": "thPna",
					"sex": "female"
				}
			],
			"group": [{
					"title": "子部门A",
					"expand": false,
					"user": [{
							"name": "Dijkstra",
							"sex": "male"
						},
						{
							"name": "Linus",
							"sex": "male"
						},
						{
							"name": "Linus",
							"sex": "male"
						}
					],
					"group": [{
						"title": "子部门AA",
						"expand": false,
						"user": [{
								"name": "小明",
								"sex": "男"
							},
							{
								"name": "Linus",
								"sex": "male"
							}
						],
						"group": []
					}]
				},
				{
					"title": "子部门B",
					"expand": false,
					"user": [{
							"name": "小明",
							"sex": "男"
						},
						{
							"name": "小红",
							"sex": "女"
						}
					],
					"group": []
				}
			]
		}

	];
	export default {
		data() {
			return {
				columns1: [{
						title: "姓名",
						key: "name",
					},
					{
						title: "性别",
						key: "sex",
					},
				],
				copyInfo: '',
				tabData: [{
						name: '王小明',
						sex: '男'
					},
					{
						name: '张小刚',
						age: '女'
					}
				],
				data1: tree,
				value: '',
				time: 0
			}
		},
		methods: {
			getUser(arr) {
				this.tabData = arr[0].user;
				this.copyInfo = arr[0].user;
				console.log(JSON.parse(JSON.stringify(arr)))
			},
			getName(val) {
				console.log(val, 'getName')
				let that = this;
				let data = that.copyInfo;
				let newArr = [];
				let copyData = data.concat();
				for(let i = 0; i < copyData.length; i++) {
					if(copyData[i].name.indexOf(val) !== -1) {
						newArr.push(copyData[i])
					}
				}
				this.tabData = newArr;
			}

		},
		mounted() {

			this.tabData = tree[0].user;
			this.copyInfo = tree[0].user;
		},
		watch: {
			"value": function(val1, val2) {
				console.log(val1, val2)
				let that = this;
				let num = that.time;
				//				that.tabData = that.copyInfo;
				let timer = setInterval(function() {
					num++
					if(num >= 2) {
						clearInterval(timer);
						that.getName(val1);
					}
				}, 100);
			}
		}

	}
</script>
<style scoped lang="less">
	#app {
		display: flex;
		width: 100%;
		.menu {
			width: 30%;
			border-right: 1px solid #000;
		}
		.right {
			width: 70%;
		}
	}
</style>
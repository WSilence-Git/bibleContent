<template>
	<view>
    <cu-custom bgColor="bg-white">
      <block slot="content">圣经目录</block>
    </cu-custom>
    <!--      tabs-->
    <view style="width: 100%">
      <scroll-view scroll-x class="bg-white nav">
        <view class="flex text-center">
          <view class="cu-item flex-sub" :class="index==xTabCur?'text-orange cur':''" v-for="(item,index) in tabList"
                :key="index"
                @tap="xTabSelect" :data-id="index">
            {{item}}
          </view>
        </view>
      </scroll-view>
    </view>

		<view class="VerticalBox" :style="[{top:CustomBar + 'px'}]">
			<scroll-view class="VerticalNav nav" scroll-y scroll-with-animation :scroll-top="verticalNavTop" style="height:calc(100vh - 280upx)">
				<view class="cu-item" :class="index==tabCur?'text-orange cur':''" v-for="(item,index) in list" :key="index" @tap="TabSelect"
				 :data-id="index">
					{{item.name}}
				</view>
			</scroll-view>
			<scroll-view class="VerticalMain" scroll-y scroll-with-animation style="height:calc(100vh - 280upx)"
			 :scroll-into-view="'main-'+mainCur" @scroll="VerticalMain">
				<view class="padding-top padding-lr" v-for="(item,index) in list" :key="index" :id="'main-'+index">
					<view class="cu-bar solid-bottom bg-white">
						<view class="action">
							<text class="cuIcon-title text-orange"></text>{{item.name}}</view>
					</view>
					<view class="cu-list menu-avatar">
						<view class="cu-item" v-for="(book,iindex) in bookList[index]" :key="iindex">

							<view class="content">
								<view class="">{{book.chapter}}</view>
							</view>
							<view class="text-lg" style="position: absolute;right: 28px">
								{{book.number}}
							</view>
						</view>
					</view>
				</view>
			</scroll-view>
		</view>
	</view>
</template>

<script>
	import SSwitch from '@/components/switch.vue'
	export default {
		components: {
		        SSwitch
		    },
		data() {
			return {
				list: [
					{
						id: 1,
						name: '创世纪',
						total:50
					},
					{
						id: 2,
						name: '出埃及记',
						total:40
					},
					{
						id: 3,
						name: '利未记',
						total:27
					},
					{
						id: 4,
						name: '民数记',
						total:36
					},
					{
						id: 5,
						name: '申命记',
						total:34
					},
					{
						id: 6,
						name: '约书亚记',
						total:24
					},
					{
						id: 7,
						name: '士师记',
						total:21
					},
					{
						id: 8,
						name: '路得记',
						total:4
					},
					{
						id: 9,
						name: '撒母耳记上',
						total:31
					},
					{
						id: 10,
						name: '撒母耳记下',
						total:24
					},
					{
						id: 11,
						name: '列王记上',
						total:22
					},
					{
						id: 12,
						name: '列王记下',
						total:25
					},
					{
						id: 13,
						name: '历代志上',
						total:29
					},
					{
						id: 14,
						name: '历代志下',
						total:36
					},
					{
						id: 15,
						name: '以斯拉记',
						total:10
					},
					{
						id: 16,
						name: '尼希米记',
						total:13
					},
					{
						id: 17,
						name: '以斯帖记',
						total:10
					},
					{
						id: 18,
						name: '约伯记',
						total:42
					},
					{
						id: 19,
						name: '诗篇',
						total:150
					},
					{
						id: 20,
						name: '箴言',
						total:31
					},
					{
						id: 21,
						name: '传道书',
						total:12
					},
					{
						id: 22,
						name: '雅歌',
						total:8
					},
					{
						id: 23,
						name: '以赛亚书',
						total:66
					},
					{
						id: 24,
						name: '耶利米书',
						total:52
					},
					{
						id: 25,
						name: '耶利米哀歌',
						total:5
					},
					{
						id: 26,
						name: '以西结书',
						total:48
					},
					{
						id: 27,
						name: '但以理书',
						total:12
					},
					{
						id: 28,
						name: '何西阿书',
						total:14
					},
					{
						id: 29,
						name: '约珥书',
						total:3
					},
					{
						id: 30,
						name: '阿摩司书',
						total:9
					},
					{
						id: 31,
						name: '俄巴底亚',
						total:1
					},
					{
						id: 32,
						name: '约拿书',
						total:4
					},
					{
						id: 33,
						name: '弥迦书',
						total:7
					},
					{
						id: 34,
						name: '那鸿书',
						total:3
					},
					{
						id: 35,
						name: '哈巴谷书',
						total:3
					},
					{
						id: 36,
						name: '西番雅书',
						total:3
					},
					{
						id: 37,
						name: '哈该书',
						total:2
					},
					{
						id: 38,
						name: '撒迦利亚书',
						total:14
					},
					{
						id: 39,
						name: '玛拉基书',
						total:4
					},
					{
						id: 40,
						name: '马太福音',
						total:28
					},
					{
						id: 41,
						name: '马可福音',
						total:16
					},
					{
						id: 42,
						name: '路加福音',
						total:24
					},
					{
						id: 43,
						name: '约翰福音',
						total:21
					},
					{
						id: 44,
						name: '使徒行传',
						total:28
					},
					{
						id: 45,
						name: '罗马书',
						total:16
					},
					{
						id: 46,
						name: '哥林多前书',
						total:16
					},
					{
						id: 47,
						name: '哥林多后书',
						total:13
					},
					{
						id: 48,
						name: '加拉太书',
						total:6
					},
					{
						id: 49,
						name: '以弗所书',
						total:6
					},
					{
						id: 50,
						name: '腓立比书',
						total:4
					},
					{
						id: 51,
						name: '歌罗西书',
						total:4
					},
					{
						id: 52,
						name: '帖撒罗前书',
						total:5
					},
					{
						id: 53,
						name: '帖撒罗后书',
						total:3
					},
					{
						id: 54,
						name: '提摩太前书',
						total:6
					},
					{
						id: 55,
						name: '提摩太后书',
						total:4
					},
					{
						id: 56,
						name: '提多书',
						total:3
					},
					{
						id: 57,
						name: '腓利门书',
						total:1
					},
					{
						id: 58,
						name: '希伯来书',
						total:13
					},
					{
						id: 59,
						name: '雅各书',
						total:5
					},
					{
						id: 60,
						name: '彼得前书',
						total:5
					},
					{
						id: 61,
						name: '彼得后书',
						total:3
					},
					{
						id: 62,
						name: '约翰一书',
						total:5
					},
					{
						id: 63,
						name: '约翰二书',
						total:1
					},
					{
						id: 64,
						name: '约翰三书',
						total:1
					},
					{
						id: 65,
						name: '犹大书',
						total:1
					},
					{
						id: 66,
						name: '启示录',
						total:22
					},
				],
				tabCur: 0,
				mainCur: 0,
				verticalNavTop: 0,
				tabList:['旧约','新约'],
				xTabCur: 0,
				scrollLeft: 0,
				load: true,
				swiperList: [{
					id: 0,
					type: 'image',
					url: 'https://qm-1251361737.cos.ap-shanghai.myqcloud.com/pro/lsg1.png'
				}, {
					id: 1,
					type: 'image',
					url: 'https://qm-1251361737.cos.ap-shanghai.myqcloud.com/pro/lsg2.png',
				}],
				arr: [
						{
							key: 1,
							value: '外卖'
						},
						{
							key: 2,
							value: '自取'
						}
					],
				foodList:[
					  {
							title1: '正味鸭掌(大份)',
							title2: '240g,鸭掌常见的食材，筋络多，皮较厚，嚼劲十足！',
							img: 'http://www.ahlsg.com/uploads/img/20180420/1524211572118346.jpg',
							price: 30,
							num:0
				        },
						{
							title1: '紫笋羊排',
							title2: '500g,紫笋羊排非常的美味，外焦里嫩，肉烂味香',
							img: 'http://www.ahlsg.com/uploads/img/20180420/1524211460181981.jpg',
							price: 55,
							num:0
						},
						{
							title1: '郑和腐竹',
							title2: '180g,油光透亮，可荤、素、烧、炒、凉拌、汤食、卤制等',
							img: 'http://www.ahlsg.com/uploads/img/20180420/1524211397906894.jpg',
							price: 20,
							num:0
						},
						{
							title1: '正山小种香干',
							title2: '200g,色泽诱人，香气扑鼻',
							img: 'http://www.ahlsg.com/uploads/img/20180420/1524211331241666.jpg',
							price: 19,
							num:0
						},
						{
							title1: '美味鸭翅',
							title2: '300g,卤鸭翅是畅销美味，鸭翅在鸭身上是非常好吃的地方',
							img: 'http://www.ahlsg.com/uploads/img/20180420/1524210197484193.jpg',
							price: 35,
							num:0
						}
				],
				bookList:[],
				totalPrice:0,
				totalNum:0,
				modalName: 0
			};
		},
		onLoad() {
      const _this = this;
      uni.getStorage({
        key: 'bookList',
        success: function (res) {
          //从缓存读取
          if (res.data){
            _this.bookList = res.data
          }
        },
        fail: function (err) {
          _this.getBookList()
        }
      });
			// uni.showLoading({
			// 	title: '加载中...',
			// 	mask: true
			// });
		},
		onReady() {

		},
		methods: {
      getBookList(){
        const _this = this;
        let bookList = []
        let count = 0
        for (let j = 0; j < this.list.length; j++){
          bookList.push([])
        }
        this.list.forEach((item, index) => {
          for (let i = 0; i < item.total; i++) {
            count = count + 1
            bookList[index][i] =
                {
                  name: item.name,
                  chapter: `第${i + 1}章`,
                  number: String(count).padStart(4, '0')
                }
          }
        })
        this.bookList = bookList
        uni.setStorage({
          key: 'bookList',
          data: _this.bookList,
          success: function () {
            console.log('缓存成功！');
          }
        });
        // uni.hideLoading()
      },
      xTabSelect(e) {
        this.xTabCur = e.currentTarget.dataset.id
        if (this.xTabCur === 0) {
          this.tabCur = 0;
          this.mainCur = 0;
          this.verticalNavTop = (0 - 1) * 50
        } else if (this.xTabCur === 1) {
          this.tabCur = 39;
          this.mainCur = 39;
          this.verticalNavTop = (39 - 1) * 50
        }
      },
			TabSelect(e) {
				this.tabCur = e.currentTarget.dataset.id;
				this.mainCur = e.currentTarget.dataset.id;
				this.verticalNavTop = (e.currentTarget.dataset.id - 1) * 50
			},
			VerticalMain(e) {
				return false
				// #ifdef MP-ALIPAY
				   return false  //支付宝小程序暂时不支持双向联动
				// #endif
				let that = this;
				let tabHeight = 0;
				if (this.load) {
					for (let i = 0; i < this.list.length; i++) {
						let view = uni.createSelectorQuery().select("#main-" + this.list[i].id);
						view.fields({
							size: true
						}, data => {
							this.list[i].top = tabHeight;
							tabHeight = tabHeight + data.height;
							this.list[i].bottom = tabHeight;
						}).exec();
					}
					this.load = false
				}
				let scrollTop = e.detail.scrollTop + 10;
				for (let i = 0; i < this.list.length; i++) {
					if (scrollTop > this.list[i].top && scrollTop < this.list[i].bottom) {
						this.verticalNavTop = (this.list[i].id - 1) * 50
						this.tabCur = this.list[i].id
						// console.log(scrollTop)
						return false
					}
				}
			}
		},
	}
</script>

<style>
	/*#ifdef H5 */
	.cu-bar.foot{bottom: 50px;}
	.bottom-modal{bottom: 100px;}
	/*#endif */
	/*#ifndef H5 */
	.bottom-modal{bottom: 50px;}
	/*#endif */

	.cu-modal {
		transition: auto;
	}
	.fixed {
		position: fixed;
		z-index: 99;
	}

	.VerticalNav.nav {
		width: 200upx;
		white-space: initial;
	}

	.VerticalNav.nav .cu-item {
		width: 100%;
		text-align: center;
		background-color: #f1f1f1;
		margin: 0;
		border: none;
		height: 50px;
		position: relative;
	}

	.VerticalNav.nav .cu-item.cur {
		background-color: #fff;
	}

	.VerticalNav.nav .cu-item.cur::after {
		content: "";
		width: 8upx;
		height: 30upx;
		border-radius: 10upx 0 0 10upx;
		position: absolute;
		background-color: #f37b1d;
		top: 0;
		right: 0upx;
		bottom: 0;
		margin: auto;
	}

	.VerticalBox {
		display: flex;
	}

	.VerticalMain {
		background-color: #fff;
		flex: 1;
	}

	.cu-list.menu-avatar>.cu-item .content {
		width: calc(100%  - 120upx);
	}
	.cu-list.menu-avatar>.cu-item{
		height: 50px;
	}
</style>

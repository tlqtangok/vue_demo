<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>vue_title</title>
		<!-- <script src="https://cdn.staticfile.org/vue/2.4.2/vue.min.js"></script> -->
		<script src="./lib/vue.min.js"></script>
		<!-- <script src="https://cdn.staticfile.org/vue-router/2.7.0/vue-router.min.js"></script> -->
		<script src="./lib/vue-router.min.js"></script>
		<!-- <script src="https://cdn.staticfile.org/axios/0.18.0/axios.min.js"></script> -->
		<script src="./lib/axios.min.js"></script>

		<style>
.id_class {
	width: 100px;
	height: 100px;
	background: green;
}


.fade-enter-active, .fade-leave-active {
    transition: opacity 2s
}
.fade-enter, .fade-leave-to /* .fade-leave-active, 2.1.8 版本以下 */ {
    opacity: 0
}

</style>

	</head>
	<body>
		<div id="el">
			<button v-on:click = "show_animation = !show_animation">show animation</button><br>
			<transition name="fade">
			<p v-show="show_animation" v-bind:style = "style_css">text for animation</p><br>
			</transition>

			<router-link to="/router_0">router_0_text</router-link>
			<router-link to="/router_1">router_1_text</router-link><br>
			<router-link v-bind:to="{path :'/router_2'}" >router_2_text</router-link>

			<h1>site : {{site}}</h1>

			<router-view><!-- will be filled with router template --></router-view>

			<br>
			<h1>url : {{url}}</h1>
			<h1 @click="click_on_h1">{{showtime()}}</h1><br>
			<span v-bind:title="msg">
				hover mouse here to see !
			</span>
			<a v-bind:href="url">{{url}}</a><br>
			<br>
			<span v-if="if_show == 1">{{ f_msg | filter_cap_first("header if_show == 1 ") | filter_cap_first("header") }}
				<p>toggle this</p>	
			</span>
			<span v-else-if="if_show == 2" >see v-else-if message</span>
			<span v-else>see else message</span>
			<br>
			<input type="text" v-model.trim="msg"><br> <!-- strim front and tail -->
			<button v-on:click="reversemsg">do reverse</button><br>
			<p v-show="if_show"> see this if_show == 1</p><br>
			<template v-for="e in id_array">
				<li> {{ e }} </li>
				<li> _______ </li>
			</template><br>

			<b v-for="e in 10"> <!-- 0..9 -->
				{{e-1}}
			</b>

			<p v-for="(k,v, idx) in id_dict">
			{{idx}}: {{ k }} , {{v}}
			</p>
			<p> {{get_computed_val}}</p>
			<button @click="id_cnt++"> id_button_text {{id_cnt}}</button><br>
			<br>
			<div>
				RMB
				<input type="text" v-model.lazy="id_rmb"> <!-- when lose focus, it will work -->
				DOLLAR	
				<input type="text" v-model.lazy="id_dollar">
			</div>
			<button v-bind:disabled="flag_diable_btn === 0">id_disable_btn</button>
			<div v-bind:class="{ id_class: flag_class}"></div>
			<br>
			<br>
			<div v-bind:class="[class_nm_0, class_nm_1]"></div>
			<div v-bind:style="{ color: id_color, fontSize: id_fontsz +'px' }">fontsz</div>

			<br>
			<input type="checkbox" id="id_0" value="v0" v-model="id_arr_checkbox"><label for="id_0">lable_0</label>
			<input type="checkbox" id="id_1" value="v1" v-model="id_arr_checkbox"><label for="id_1">label_1</label>
			<input type="checkbox" id="id_2" value="v2" v-model="id_arr_checkbox"><label for="id_2">label_2</label>
			<p>{{ id_arr_checkbox }}</p>

			<input type="radio" id="id_r0" value="v_r0" v-model="id_radio_picked"><label for="id_r0">lable_r0</label>
			<input type="radio" id="id_r1" value="v_r1" v-model="id_radio_picked"><label for="id_r1">lable_r1</label>
			<input type="radio" id="id_r2" value="v_r2" v-model="id_radio_picked"><label for="id_r2">lable_r2</label><p>{{id_radio_picked}}<br>

			<select v-model="id_select" name="name_sites">
				<option value="">选择一个网站</option>
				<option value="www.algoers.com">algoers.com</option>
				<option value="www.google.com">Google</option>

			</select><p>{{id_select}}</p>

			<html_label_component v-bind:sub_bind_name="id_from_parent_to_sub"></html_label_component>	
			<br>
			<div v-jidor="{color:'green', text:'v-jidor-text'}"></div>
			<p>{{res_from_srv}}</p><br>

			<p @click="get_json_json()"><button>get_json_json</button>  {{res_from_srv_via_click}}</p>
			<p @click="post_json_json()"><button>post_json_json</button>  {{res_from_srv_via_click_post}}</p><br>
			<p @click="multiple_request()"><button>multiple_request</button> {{id_multiple_request}}</p><br>
			<span v-html="id_test_html"><span>


		</div>

		<script type="text/javascript">

			const router = new VueRouter({
				routes: [
					{path:'/router_0',component:{template: '<div>router_0</div>'} },
					{path:'/router_1',component:{template: '<div>router_1</div>'} }
				]	
			})

			var id_component = {
				props: ['sub_bind_name'],
				template: '<h3>html_label_component {{ "abc----" + sub_bind_name}}</h3>'	
			}

Vue.directive('jidor', function(el, binding)
	{
		el.innerHTML = binding.value.text
		el.style.backgroundColor = binding.value.color
	}
)

var app = new Vue({
	router,

	el: '#el',
	data: {
		id_test_html: "<h1>id_test_html</html>",
		res_from_srv : "NULL",
		res_from_srv_via_click:null,
		res_from_srv_via_click_post:null,
		id_multiple_request:"NULL",

		show_animation : true,
		style_css :{
			fontSize: '30px',
			color:'red'
		},

		id_from_parent_to_sub: "id_from_parent_to_sub_text",
		id_select:"",
		id_radio_picked : "v_r1",
		id_arr_checkbox:[],
		id_color:'blue',
		id_fontsz:22,
		site: "snoob",
		url: "https://www.baidu.com",
		alexa: "10000",
		msg:"id_msg",
		f_msg: "old_f_msg",
		if_show: true,
		id_array: ["p0", 1, 33333],
		id_cnt: 0,
		id_dict :
		{
			"k0":"v0",
			"k1":"v1",
			"k2":"v2",
		},
		id_rmb:0,
		id_dollar:0,
		flag_diable_btn:0,
		flag_class:1,
		class_nm_0:"id_class", 
		class_nm_1:"id_class",
	},  // end data{}
	mounted (){
		axios.get('./json.json')
			.then(res =>{this.res_from_srv=res; /*res.data*/})	
			.catch(function(error){console.log(error);});
	},

	filters: { 
		filter_cap_first: function(value, value2)
		{
			if (!value) return ''
			value = value2 + value.toString() 
			return value.charAt(0).toUpperCase() + value.slice(1)	
		}
	},
	computed: { 
		get_computed_val: function()
		{
			return this.msg + " + " + this.msg;
		}

	},
	watch:{

		id_rmb: function(val_new)
		{
			this.id_rmb = val_new; 
			this.id_dollar = val_new / 6.99; 
		},
		id_dollar: function(val_new)
		{
			this.id_rmb = val_new * 6.99; 
			this.id_dollar = val_new; 
		}
	},

	methods: {
		showtime: function() 
		{
			return  this.site + " - in function, time " + new Date().toLocaleString();
		},
		reversemsg: function()
		{
			this.msg = this.msg.split('').reverse().join('');	
		},
		click_on_h1: function()
		{
			this.msg = "-click on " + new Date().toLocaleString();	
		},

		post_json_json: function()
		{
			/*
				axios.request({
				method: 'post',
					url: '/xxxx/yyyy', 
					data: {
					d0: 'v_d0', d1: 'v_d1'
					}
				}).then().catch();
			*/
			// from this._data sub a key [this.res_from_srv_via_click_post], how to ?
			var this_data_copy_remove_this_post = JSON.parse(JSON.stringify(this._data)); 
			delete this_data_copy_remove_this_post.res_from_srv_via_click_post; 
			//console.dir(this_data_copy_remove_this_post);
			var string_repeat = "X"; 
			string_repeat = string_repeat.repeat(1*128); 
			this_data_copy_remove_this_post.string_repeat = string_repeat; 


            axios.post( './json.json?k0=v0&k1=v1', { "post_params":{"k0_post":"v0_post"},  "app_all_data":this_data_copy_remove_this_post} )   // don't merge the json, but string all of the query k0 k1 k0
				.then(res =>{ this.res_from_srv_via_click_post =res; /*res.data*/ })	
				.catch(function(error){console.log(error);});
		},

		get_test_0:function(){return axios.get("./json.json");}, 
		get_test_1:function(){return axios.get("./json.json");},

		multiple_request: function(){
			axios.all([(this.get_test_0)(), (this.get_test_1)()])
				.then(axios.spread((_1, _2) => {
					console.dir(_1);
					console.dir(_2);

					this.id_multiple_request = JSON.stringify(_1) + "_____________ABC______________\n\n" + _2.data; 
				}));
		},

		get_json_json: function()
		{
			axios.get( './json.json?k0=v0&k1=v1', { params:{"k0":"v0"} })   // don't merge the json, but string all of the query k0 k1 k0
				.then(res =>{this.res_from_srv_via_click =res.data; /*res.data*/})	
				.catch(function(error){console.log(error);});
		},



	},

	components: {
		'html_label_component':id_component ,
	},

}

)

app.$watch('id_cnt' , function(v_new,v_old){alert("id_cnt from " + v_old + " to " + v_new);});


setTimeout(
    function(){
        //app.id_cnt += 20;  // change any data, will refresh whole data
		console.log("time it"); 
    },40000
);
		</script>
	</body>
</html>


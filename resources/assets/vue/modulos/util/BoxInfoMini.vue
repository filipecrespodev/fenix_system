<template>

	<div class="col-lg-3 col-md-6 col-xs-12" v-if="modal" >
		<div class="info-box" @click="$modal.show(''+modal+'')" :style="(link!='')?'cursor: pointer;':''">
			<a style="color: #333;" @click="$modal.show(''+modal+'')">
				<span class="info-box-icon" :style="'background-color:'+boxColor">
					<i class="fa" :class="'fa-'+icone" :style="'color:'+iconeColor" ></i>
				</span>
				<div class="info-box-content" :style=" download == 'true' ? 'padding-bottom: 3px;' : '' "> 
					<span class="info-box-text">
							{{ titulo }}
					
					<i v-if="download == 'true' && canDownload == true" style="font-size: 12px;" @click="downloadExcel($event, referencia)" class="fa fa-download pull-right text-muted btn btn-box-tool posicaoDownload" ></i> 
					</span>

					<span class="info-box-number">
						<span style="font-size:40px; color: #333;" :class="classe">
							{{ content }}
						</span>
						<!-- <span class="pull-right visible-lg" style="font-size:30px; margin-top: 12px;"> -->
						<span class="pull-right" v-if="alert > 0" style="font-size:30px; margin-top: 12px;">
							<i class="fa fa-bell" style="color:#dd4b39" ></i>
						</span>

					</span>
				</div>
			</a>
		</div>
	</div>	
	<div class="col-lg-3 col-md-6 col-xs-12" v-else-if="status">
		<div class="info-box">
			<a style="color: #333;">
				<span class="info-box-icon" :style="'background-color:'+boxColor">
					<i class="fa" :class="'fa-'+icone" :style="'color:'+iconeColor" ></i>
				</span>
				<div class="info-box-content" :style=" download == 'true' ? 'padding-bottom: 3px;' : '' "> 
					<span class="info-box-text">
							{{ titulo }}
					
					</span>

					<span class="info-box-number">
						<span style="font-size:30px;color:#333; width:65%" class="truncate" :class="classe">
							<span>
								{{ msgStatusAtual }}
								
							</span>
						</span>
											
						<span class="pull-right" style="padding:5px 0px" >
							<label class="switch" style="margin-top: 5px;">
								<input name="atualiza" v-model="statusAtual" type="checkbox"> 
								<span class="slider round" @click="alteraStatus"></span>
							</label>
						</span>
						
					</span>
				</div>
			</a>
		</div>
	</div>	
	<div class="col-lg-3 col-md-6 col-xs-12" v-else>
		<div class="info-box">
			<a style="color: #333;" :href="link" :style="(link=='')?'cursor: auto;':''">
				<span class="info-box-icon" :style="'background-color:'+boxColor">
					<i class="fa" :class="'fa-'+icone" :style="'color:'+iconeColor" ></i>
				</span>
				<div class="info-box-content" :style=" download == 'true' ? 'padding-bottom: 3px;' : '' "> 
			
					<div class="col-md-12" style="padding:0px;">
						<div class="col-md-10" style="padding:0px;" data-toggle="tooltip" data-placement="top" :title="tooltip">
							<span class="info-box-text "> 
									{{ titulo }}
							</span>
						</div>
						<div class="col-md-2" style="padding:0px;">					
							<i v-if="download == 'true' && canDownload == true" style="font-size: 12px;" @click="downloadExcel($event, referencia)" class="fa fa-download pull-right text-muted btn btn-box-tool posicaoDownload firefoxPosicao" ></i> 
						</div>						
					</div>						
				

					<span class="info-box-number">

						<span style="font-size:37px; color: #333; width: 80%;" class="truncate" :class="classe" :title="content">
							{{ content }}
						</span>
						
						<span class="pull-right" v-if="alert > 0" style="font-size:30px; margin-top: 12px;">
							<i class="fa fa-bell" style="color:#dd4b39" ></i>
						</span>

					</span>
				</div>
			</a>
		</div>
	</div>	

</template>

<script>

	export default {
		 props:['download', 'canDownload', 'icone', 'iconeColor' ,'boxColor', 'titulo', 'content', 'contentAlert', 'alert', 'link', 'referencia', 'modal', 'tooltip', 'classe', 
		 	'status', 'parametrosVerdadeiro', 'parametrosFalso'],

		data () {
            return {
                pages:[],
                item:[],
				statusAtual:'',
				msgStatusAtual: ''
            }
        },
        watch:{
        	content: function (val){        		
				this.statusAtual = this.content
			},
			statusAtual: function(val){
				this.msgStatusAtual = ( this.statusAtual ? this.parametrosVerdadeiro : this.parametrosFalso)				
				
			}
        },
        methods:{
			downloadExcel(ev, excel){
				
				ev.preventDefault()
                this.$emit('downloadExcel', excel)
	
         	},
			alteraStatus(){				
				this.statusAtual = !this.statusAtual
				this.$emit('alteraStatus', this.statusAtual )	
			}

        },
        mounted(){			
        }
	};

</script>

<style>
    @-moz-document url-prefix() { 
        .firefoxPosicao {
            padding-top: 26px;
        }
    }
</style>





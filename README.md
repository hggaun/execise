1   头部
<xpa-header #header [headerConfig]="headerConfig"></xpa-header> 
@ViewChild('header') header:XpaHeaderComponent
headerConfig:IHeaderConfig//buttons blueButton clickEvent
    {
        button:[
            {type:ButtonType.Common,title,class}
        ]
    }
this.headerConfig.clickEvent.subscribe((title)=> title为名称)

2   表格
<xpa-table #xpaTableSku [tableConfig]="tableConfig"></xpa-table>
@ViewChild('xpaTableSku') xpaTable:XpaTableComponent
tableConfig:any=new TableConfig(TableConfigType.mainTable,
  [
    {dataField,caption,alignment,cellType,cellTemplatecellExtra:{fields:['code','shortName'],diffColor:true}}   
  ],
  {Self:this,bizType,keyExpr,height,
    dataSource:new CustomStore({
        key,
        load:async function (loadOptions:any){
            loadOptions.bizType = ''
            loadOptions.filters = [{
                name:'',value:
            }]
            // 获取数据接口
            let resp=await lastValueFrom(this.transService.loadPolicies(loadOptions));
            resp.items.forEach(item=>{
                进行数据更正
            })
            return {
                //返回数据
                data:resp.items,
                totalCount:resp.totalCount
            }
        }
    }),
    toolbarConfig:[{position,type:ToolType.Search,placeholder,key,value,
            dataSource,displayExpr,valueExpr
    }],
    //子表
    children:[
        new TableConfig(TableConfigType.subTable,[
            {dataField,caption,}],
            {Self:this,bizType,height,keyExpr}
            )
    ]
})
    this.tableConfig.event.subscribe(evt=>{
        evt.type --- onRowDblClick RowClick initFocusItem afterKeyDown
    })
    this.tableConfig.toolbarEvent.subscribe({from,type,config,key,value,leftFilters,rightFilters})=>{
        type--事件类型   config--配置对象      key--配置对象中的key
        leftFilters--左侧header部分的变化值    rightFilters--右侧header部分的变化值
    }

3      标签
<xpa-tabs #xpaTabs 
        [tabsConfig]="tabsConfig" 
        (event--事件发射器)="tabsEvent($event)"
        [templates]="{skuTemplate:templateSku}"   </xpa-tabs>
<ng-template #templateSku> -- 模版
@ViewChild('xpaTabls') xpaTabs: XpaTabsComponent 
tabsConfig:any={
    isDrawer:true,
    tabs:[
        {
            title:'名称',
            config:{配置属性}
        },
        {
            第二个
        }
    ]
}
tabsEvent(evt){evt.type=='',执行操作}
// 获取表单配置数据
this.dataServiceloadForm({page,role})=>{
    tabsConfig.tabs[0].config={form:res.items}  //对象里有form与82行对应
    在xpa-tabs中   有this.ComponentRef.instance.formConfig=this.tabsConfig.tabs[index].config
    其中formConfig的接口是IFormConfig，它有4个属性   self,bizType,form,disabled
}


4   表单类型抽屉  
initFormDrawer()---表单抽屉
    this.drawerService.create({
        nzTitle,nzWidth,nzContent:XpaFormComponent,nzButtons[],
        beforeOpen:(com:XpaFormComponent)=>{
            com.formConfig=<IFormConfig>{
                Self,bizType,form:表单配置
            }
            com.initFormConfig().then((res:any)=>{
                res.configs
                createForm({bizType}).subscribe(res=>{
                    com.nativeDS['']=res.['']
                    if(title.startsWith('编辑')){
                        获取选中单元格的数据
                        data=this.xpaTable.dataGrid.instance.getSelectedRowData()[0]
                        com.formData=data
                    }
                })
                configs.forEach(item=>{
                    item.fieldName=='' {
                        item.onValueChanged=e=>{
                            当表单某个部分发生变化时  执行函数  
                        }
                    }
                })
            })

        },
        buttonClick:(ref:NgxDrawerComponent,dialog:XpaFormComponent,button:NgxDrawerButton)=>{
            button.label=='确定'
            获取表单数据
            data=dialog.getFormData() 需要转换的数据要进行转换
            dialog.validata().then(res=>{
                //若表单内容规范则提示成功
                if(res){
                    调用更新接口 
                    this.render.success('').then(()=>{
                        //  更新表格中的数据   需要dataSource为customeStore类(load方法)
                        this.xpaTable.dataGrid.instance.refresh().then(()=>{
                                // 表格刷新之后执行函数、
                            this.xpaTable.dataGrid.instance......
                        })
                    })
                }
            })
        }
    })

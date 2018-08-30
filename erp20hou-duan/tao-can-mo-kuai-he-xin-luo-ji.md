# 套餐模块核心逻辑

##### 1.套餐模块表的关系

![](/assets/combo_db.png)

##### 2.微信小程序针对代理商套餐列表

源码

```
     /**
     * 根据条件查询代理商标签
     * @param agentId
     * @param comboModel
     * @return
     */
    private List<AgentTagModel> queryAgentTagListByCondition(Integer agentId,ComboModel comboModel){

        //1.获取套餐下的售卖区域
        List<SellAreaModel> sellAreaModelList = comboModel.getSellAreaModelList();
        //2.获取销售区域的省，下面没有市，没区
        List<String> provinceIds = sellAreaModelList.stream().filter( sellAreaModel -> {
            if(!StringUtils.isEmpty(sellAreaModel.getProvinceId()) 
            && StringUtils.isEmpty(sellAreaModel.getCityId()) 
            && StringUtils.isEmpty(sellAreaModel.getAreaId())){
                return true;
            }
            return false;
        }).map(SellAreaModel::getProvinceId).collect(Collectors.toList());
        //3.获取销售区域的市,下面没有区
        List<String> cityIds = sellAreaModelList.stream().filter( sellAreaModel -> {
            if(!StringUtils.isEmpty(sellAreaModel.getProvinceId()) 
            && !StringUtils.isEmpty(sellAreaModel.getCityId()) 
            && StringUtils.isEmpty(sellAreaModel.getAreaId())){
                return true;
            }
            return false;
        }).map(SellAreaModel::getCityId).collect(Collectors.toList());
        //4.获取销售的区
        List<String> areaIds = sellAreaModelList.stream().filter( sellAreaModel -> {
            if(!StringUtils.isEmpty(sellAreaModel.getProvinceId()) 
            && !StringUtils.isEmpty(sellAreaModel.getCityId()) 
            && !StringUtils.isEmpty(sellAreaModel.getAreaId())){
                return true;
            }
            return false;
        }).map(SellAreaModel::getAreaId).collect(Collectors.toList());
        SaleRuleModel saleRuleModel = comboModel.getSaleRuleModel();
        //5.独家非独家
        Integer soleAgency = saleRuleModel.getSoleAgency();
        //限定的代理商级别
        List<Integer> agencyLevels = saleRuleModel.getSaleTagModelList().stream().filter(saleTagModel -> {
            return saleTagModel.getTagType().equals(SalesRuleStatusEnum.AGENCY_LEVEL_TAG.getCode());
        }).map(SaleTagModel::getTagId).collect(Collectors.toList());
        //6.限定项目id编号
        List<Integer> buyProjectIds = saleRuleModel.getSaleTagModelList().stream().filter(saleTagModel -> {
            return saleTagModel.getTagType().equals(SalesRuleStatusEnum.AGENCY_BUY_PROJECT_TAG.getCode());
        }).map(SaleTagModel::getTagId).collect(Collectors.toList());
        AgentFilterParam agentFilterParam = new AgentFilterParam();
        agentFilterParam.setProvinceList(provinceIds);
        agentFilterParam.setCityList(cityIds);
        agentFilterParam.setAreaList(areaIds);
        agentFilterParam.setAgentId(agentId);
        agentFilterParam.setSoleAgency(soleAgency);
        agentFilterParam.setAgencyLevelList(agencyLevels);
        agentFilterParam.setBuyProjectList(buyProjectIds);
        List<AgentTagModel> agentTagModelList = agentTagMapper.queryAgentTagByCondition(agentFilterParam);
        return agentTagModelList;
    }
```

###### 因为微信小程序是只针对代理商和地推人员的，所以对这两类人员有很多限制

##### 限制条件:

1.必需上上线的套餐

2.必需是在售卖时间内的套餐

3.必需是针对代理商的而不是其他人员的限制\(可以查看表中的一个属性is\_agency\_all=1\)

**前三条限制是必需的，下面的限制会根据操作人员的设定而变动**

4.当前套餐的售卖区域,包括省份、市、和地区他们之间是或者的关系

5.会限定当前代理商的是否是独家代理商可以购买

6.会限定代理商的级别，那些代理商级别的可以购买改套餐\(比如:意向商，A级商等\)

**通过上面的限定条件要去代理商标签表\(lb\_agent\_tag\)中查询是否有记录,如果有表示该套餐当前代理商可以购买**

##### 3.微信小程序针对销售员套餐列表

源码

```
public  Map<String, List<ComboVo>> salesmanFilterCondition(Integer salesmanId) {
        List<ComboModel> comboModelList = comboMapper.querySalesmanFilterCondition();
        List<ComboModel> comboModelListFilter = comboModelList.stream().filter(comboModel -> {
            //限定代理商代理过的套餐
            if(ObjectUtils.isEmpty(comboModel.getSaleRuleModel())){
                return false;
            }
            List<Integer> saleManIds = comboModel.getSaleRuleModel()
            .getSaleTagModelList().stream().filter(saleTagModel -> {
                return saleTagModel.getTagType().equals(SalesRuleStatusEnum.SALE_MAN_TAG.getCode());
            }).map(SaleTagModel::getTagId).collect(Collectors.toList());
            if(CollectionUtils.isEmpty(saleManIds)){
                return true;
            }
            return saleManIds.contains(salesmanId);
        }).collect(Collectors.toList());
        Map<String, List<ComboVo>> subjectGroup = comboModelListFilter.stream().map(comboModel -> {
            return convertComboVo(comboModel);
        }).collect(Collectors.groupingBy(comboVo ->{
            return comboVo.getSubjectionProjectName().trim();
        }));
        return subjectGroup;
    }
```

**限制条件:**

1.必需上上线的套餐

2.必需是在售卖时间内的套餐

3.必需是针对代理商的而不是其他人员的限制\(可以查看表中的一个属性is\_sale\_man=1\)

4.当前的销售人员id必需在我们的限定表\(lb\_\_sale\_\_tag\)中有，如果没有表示改套餐当前销售员不能买

还有一种情况，就是如果改套餐在限定表中没有记录并且is\_sale\_man=1表示所有销售员都可以购买

##### 问题联系人:

作者:张业婷

邮箱: zhangyeting@lbonline.cn






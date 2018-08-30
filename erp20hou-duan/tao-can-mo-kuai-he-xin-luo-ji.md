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
            if(!StringUtils.isEmpty(sellAreaModel.getProvinceId()) && StringUtils.isEmpty(sellAreaModel.getCityId()) && StringUtils.isEmpty(sellAreaModel.getAreaId())){
                return true;
            }
            return false;
        }).map(SellAreaModel::getProvinceId).collect(Collectors.toList());
        //3.获取销售区域的市,下面没有区
        List<String> cityIds = sellAreaModelList.stream().filter( sellAreaModel -> {
            if(!StringUtils.isEmpty(sellAreaModel.getProvinceId()) && !StringUtils.isEmpty(sellAreaModel.getCityId()) && StringUtils.isEmpty(sellAreaModel.getAreaId())){
                return true;
            }
            return false;
        }).map(SellAreaModel::getCityId).collect(Collectors.toList());
        //4.获取销售的区
        List<String> areaIds = sellAreaModelList.stream().filter( sellAreaModel -> {
            if(!StringUtils.isEmpty(sellAreaModel.getProvinceId()) && !StringUtils.isEmpty(sellAreaModel.getCityId()) && !StringUtils.isEmpty(sellAreaModel.getAreaId())){
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





##### 3.微信小程序针对销售员套餐列表




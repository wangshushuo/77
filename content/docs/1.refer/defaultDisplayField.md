# defaultDisplayField

EntityGraphQLQueryBuilder.ts中setQuickSearch方法会将entity.defaultDisplayField做为查询条件
    ```
    const { queryOptions } = this.queryTree;

    let baseCriteriaStr = this.baseCriteriaStr;
    const keywordCriteriaStr = [];

    const { supressDefaultDisplayField = false } = queryOptions
    if (this.entity.defaultDisplayField && !supressDefaultDisplayField) {
      keywordCriteriaStr.push(`${this.entity.defaultDisplayField} LIKE '%${keyword}%'`);
    }
    ```

预制数据-业务对象中勾选的默认显示会被放到entity.defaultDisplayField
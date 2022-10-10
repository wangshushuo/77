---
title: "单元测试 Mock"
date: 2022-07-25T14:19:57+08:00 
author: 
---

## common

### advance-grid

```ts
jest.mock('@athena-ui/components/ag-grid/entities/colDef');
jest.mock('@components/advance-grid')
jest.mock('@components/advance-grid', () => {
    return {
        CommonUsedActions: {
            view: {
                click: jest.fn((rowIndex, data) => {
                    return {
                        onClick: jest.fn()
                    }
                })
            }
        }
    }
})
```

### 路由

```ts
const appRouterHashManager = {
    generateHash: jest.fn()
}

const proxyHistory = {
    push: jest.fn(),
}

jest.mock('@root/router-manager', () => {
    return {
        appRouterHashManager: {
            generateHash: (...options) => appRouterHashManager.generateHash(...options)
        }
    }
});

jest.mock('@root/router-history', () => {
    return {
        default: {
            push: (...option) => proxyHistory.push(...option)
        }
    }
});
```

### checkAuth

```ts
const checkAuth = jest.fn((resourceId: string, actionId: string) => {
    return true;
})
jest.mock('@root/func-auth', () => {
    return {
        checkAuth: (a, b) => {
            return checkAuth(a, b);
        }
    }
});
```

### 其他

```ts
jest.mock('@axios');
jest.mock('axios');
jest.mock('react');
jest.mock('@q7/athena-gen/lib');
jest.mock('@q7/metadata/lib');
```

## bizform

### easy-bizform

```ts
jest.mock('@main/components/easy-bizform', () => {
    const data = {
        task: {
            deliverable: [{
                description: '被我',
                id: 'BGTUGV52B7J0025',
                isRequired: false,
                name: '害得我',
                task: {
                    deliverablesCount: 0,
                    id: 'V5WDUU51EP10003',
                    name: '阶段三',
                }
            }],
        }
    };
    return {
        EasyBizFormItemsPresenter: class {
            get formValue() {
                return data
            }

            protected emptyDeliverable = () => {
                data.task.deliverable = null
            }
        }
    }
})

jest.mock('@main/components/easy-bizform', () => {
    return {
        EasyBizFormPresenter: class {
            constructor() {
            }

            private form = {
                select: (field) => {
                    return {
                        value: {
                            billType: {
                                funcUnits: [
                                    {
                                        funcUnit: FuncUnit_Constants.projectStageExecuteDateValidator,
                                        setting: true
                                    }
                                ]
                            }
                        },
                    }
                }
            }

            private getMode() {
                return 'Create'
            }
        }
    }
})

jest.mock('@main/components/easy-bizform', () => {
        const mock = {
            EasyBizFormPresenter: class {
                constructor() {
                }
            }
        }
        mock.EasyBizFormPresenter.prototype.getOtherFormOptions = (...option) => EasyBizFormPresenter.getOtherFormOptions(...option);
        mock.EasyBizFormPresenter.prototype.getDataOptions = (...option) => EasyBizFormPresenter.getDataOptions(...option);
        return mock;
    }
);

jest.mock('@components/form-layout', () => {
    return {
        MSTFormElement: class {
        }
    }
})

jest.mock('@root/solutions/biz-form/page/menu-buttons/create', () => {
    return {
        CreateCreator: class {
            constructor() {
            }
        }
    }
})
```

### biz-form

```ts

jest.mock('@root/solutions/biz-form', () => {
    return {
        BizFormPresenter: class {
        },
        BeanNames: class {
        },
        BizFormModeEnum: class {
        },
        DataOptions: class {
        },
        DisplayOptions: class {
        },
        EditOptions: class {
        },
        FieldStatusControlEnum: class {
        },
        RangeWalkOptions: class {
        },
    }
})

```

## 列表

```ts
const presenter = {
    toolbarConnector: {
        makeCreateButton: jest.fn((options: IMakeCreateButtonOptions): CommandBarTypes => {
            return options;
        })
    },
    listSolutionConnector: {
        rowActionController: {
            makeRowViewAction: jest.fn(),
        },
    },
}

const QueryListPagePresenter = {
    getListOption: jest.fn(),
    getQueryListOption: jest.fn(),
}

jest.mock('@root/solutions/athena-solutions/query-list');
jest.mock('@root/solutions/query-solution');

jest.mock('@main/screens/list', () => {
    const mock = {
        QueryListPagePresenter: class {
            presenter = presenter;
        }
    }
    mock.QueryListPagePresenter.prototype.getListOption = (...option) => QueryListPagePresenter.getListOption(...option);
    mock.QueryListPagePresenter.prototype.getQueryListOption = (...option) => QueryListPagePresenter.getQueryListOption(...option);
    return mock;
});
jest.mock('@root/solutions/athena-solutions/query-list/components/toolbar', () => {
    return {
        ToolbarActionGroup: {},
    }
});
```

### 动态表单文档
###### 特性
1. 支持 ***答案回显***
2. 支持对特定格式的数据结构 ***多对多*** 控制问题显/隐与提交对应答案与否

###### 结构
1. 获取动表
```typescript
// 接口结构须与 questionnaire 一致
export interface questionnaire { // 整个表单数据，包含各个题目
    hasAnswer: boolean, // 该表单是否已经被提交过
    questions: questions[],
    [propName: string]: any // 其余字段
}
interface questions { // 单个问题
    allAttributeResponse: allAttributeResponse, // 所有题目属性
    answerOne: string, // 单选/文字/日期时间 所选答案 
    answerTwo: string, // (暂时不需要)
    answerType: number, // 
    dataType: number, // 题目类型
    dataTypeName: string, // 题目类型名称
    files: files[] // 文件储存结构
    hasAnswer: boolean, // 该题目是否已经被提交过
    logicCode2: string, // 与questionCode一致
    multipleSelectoptions: multipleSelectoptions[],// 多选选项
    questionCode: string, // 题目id
    questionName: string, // 题目名称
    questionnaireCode: string, // 表单id
    selectOptions: selectOptions[]| null, // 单选选项
    showRuleCondition?: any, // 废弃
    showRuleNew: showRuleNew,// 控制规则
    viewIndex: number
}

interface commonAttribute { // 公共属性
    helpInfo?: string, // 题目注解
    isRequired: boolean, // 是否必填
    isShow: boolean // 初始化是否显示
}
interface dateDayAttribute { // 日期类型-精确到天

}
interface dateDayTimeAttribute { // 日期类型-精确到秒
    endDayTime?: string,
    startDayTime?: string
}
interface decimalsNumAttribute { // 小数类型
    isStepStrictly?: boolean,
    numPrecision?: number,
    max?: number,
    min?: number,
    step?: number
}
 interface fileAttribute { // 文件属性
    fileLimitNum?: number,
    fileLimitSize?: number,
    fileType?: string
}
interface mutipleSelectAttribute { // 多选属性
    limitSelectNum?: number
}
 interface numAttribute { // 整数属性
    max?: number,
    min?: number,
    step?: number
}
 interface textAttribute { // 文本属性
    maxLength?: number,
    minLength?: number,
}
interface allAttributeResponse { // 所有题目相关属性
    commonAttribute: commonAttribute
    dateDayAttribute?: dateDayAttribute,
    dateDayTimeAttribute?: dateDayTimeAttribute,
    decimalsNumAttribute?: decimalsNumAttribute,
    fileAttribute?: fileAttribute,
    mutipleSelectAttribute?: mutipleSelectAttribute,
    numAttribute?: numAttribute,
    textAttribute?: textAttribute,
}
interface files { // 文件结构
    fileName: string,
    fileType: number,
    fileUrl: string
}
interface multipleSelectoptions { // 多选选项
    answerOptionCode: string, // 选项value
    answerOptionName: string // 选项key
}
interface selectOptions { // 单选选项
    isDefaultChoice: boolean,
    logicCode: string, // 选项value
    logicCode2?: string, // 同logicCode
    optionIndex: number, // 选项顺序
    optionValue: string, // 选项key
    questionCode: string

}
 interface showRuleNew { // 控制规则
    detailAnds: detailAnds[], // and 规则
    detailOrs: detailOrs[], // or规则
    isShow: boolean, // 满足规则后显示与否
    questionnaireCode?: string, // 表单id
    resultQuestionCode?: string // 被控制的问题id
}
 interface detailAnds { // and规则
    conditionOptionCode: string // 选项id
    conditionQuestionCode: string // 题目id
    conditionTwoType: string // 等价关系 （目前仅支持==“）
}
 interface detailOrs { // or规则
    conditionOptionCode: string // 选项id
    conditionQuestionCode: string // 题目id
    conditionTwoType: string // 等价关系 （目前仅支持==“）
}
```
2. 上传图片/文件
```typescript
// 上传图片接口返回须与此一致
export interface returnFileStucture { // 接口返回的结构
    code: number,
    data: returnFile,
    [propsName: string]: any
}
interface returnFile { // 
    fileName: string,
    fileUrl: string,
    fileUniqueKey: string,
}
```

### 提交表单（入参）数据结构
```typescript
interface answer { // 单个题目
    dataType: number, // 题目类型
    answerOne: string | number, // 题目选项值
    answerTwo: string,  // （暂不使用）
    files: { 
        fileName: string,
        url: string,
        [propName: string]: any
    }[],
    optionCodes: string[], // 多选题答案数组
    questionCode: string, // 题目id
    logicCode2: string // 同questionCode
}
export const finalAnswers: answers[] // 最后提交答案的数组
```
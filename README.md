公共小部件和辅助类
===========

## 数据表格

基于[DataTables](https://datatables.net)

### 固定表头

```php
echo \xlerr\common\widgets\DataTable::widget([
    'dataTableOptions' => [
        'fixedColumns' => [
            'leftColumns'  => 2,
            'rightColumns' => 1,
        ],
        'scrollY' => '300px', // 表格高度控制, 默认为: false
    ],
    'dataTableEvents'  => [
        'init.dt' => 'function () { console.log(\'init\'); }',
    ],
    'dataProvider' => new \yii\data\ArrayDataProvider([
        'allModels' => [],
    ]),
    'columns' => [],
]);
```

## 自定义格式化方法

### 注册

```php
'components' => [
    'formatter' => [
        'as CustomFormatter' => \xlerr\common\behaviors\FormatterBehavior::class,
    ],
];
```

### 金额格式化

- f2y|y2f 用法

    ```php
    $formatter = \Yii::$app->getFormatter();
    $formatter->format(123456, ['f2y', true]); // string 1,234.56
    $formatter->format(123456, 'f2y'); // float 1234.56
    $formatter->format(1234.56, 'y2f'); // int 123456
    ```

- f2y|y2f 用法 - \yii\grid\GridView

    ```php
    'columns' => [
        [
            'format' => ['f2y', true],
            'attribute' => 'amount',
        ],
    ],
    ```
    `amount`为`647283`, 输出字符串`6,472.83`

- in 用法

    ```php
    'columns' => [
        [
            'format' => ['in', ['open' => '打开', 'close' => '关闭'], 'defaultValue'],
            'attribute' => 'status', // print 打开|关闭|defaultValue
        ],
    ],
    ```

### 金额输入框

![amount_input](./amount_input.png)

`amount`字段值单位为分, 文本框内值的单位为元

```php
$form->field($model, 'amount')->widget(\xlerr\common\widgets\MoneyInput::class, [
    'options' => [
        'placeholder' => '金额输入框',
    ],
]);
```

or

```php
\xlerr\common\widgets\MoneyInput::widget([
    'name' => 'amount',
    'options' => [
        'placeholder' => '金额输入框',
    ],
]);
```

### 表单

提交表单等待效果

![submit_waiting](./submit_waiting.png)

```php
echo \xlerr\common\widgets\ActiveForm::begin([
    'submitWaiting' => true,
]);
```
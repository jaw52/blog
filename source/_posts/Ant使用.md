---
title: Ant使用
tags:
- ant
- 第三方库
categories: 
- 前端
---

# Ant v3.0

## Form

### 只在提交时做验证

有时候我们只需要在提交时验证表单，不需要在每一步都验证表单时可以如下设置

`this.props.form` 提供的 API中`setFields`，用来设置一组输入控件的值与错误状态

在`onSubmit`提交前验证一下表单，并且`setFields`设置错误信息就可以了

```js
onSubmit = (e) => {
    e.preventDefault();
    this.props.form.validateFields((error, values) => {
      if (!error) {
        console.log('ok', values);
        setTimeout(() => {
          // server validate
          if (values.user === 'yiminghe') {
            this.props.form.setFields({
              user: {
                value: values.user,
                errors: [new Error('forbid ha')],
              },
            });
          }
        }, 500);
      } else {
        console.log('error', error, values);
      }
    })
```


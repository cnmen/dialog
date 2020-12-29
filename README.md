# Dialog
## 统一Dialog风格

版本：1.0.0<br>
作者：西门提督<br>
日期：2020-12-28

## Dialog框架用法如下，以RecyclerView为例：

### DialogHelper说明：
new DialogHelper.Builder(this)
        .title(R.string.app_name) // 标题文字
        .titleGravity(GravityEnum.START) // 标题居中
        .titleSize(25)
        .titleColorRes(R.color.orange_dark) // 标题颜色

        .iconRes(R.mipmap.ic_launcher) // 设置标题左侧图标
        .limitIconToDefaultSize() // 将显示的图标大小限制为48dp

        .content("测试Dialog内容，测试Dialog内容，测试Dialog内容，测试Dialog内容，测试Dialog内容")
        .contentGravity(GravityEnum.START) // 内容总体位置
        .contentSize(12)
        .contentColorRes(R.color.green_dark) // 内容颜色

        .positiveText(android.R.string.ok) // 确定
        .okSize(15)
        .positiveColorRes(R.color.black) // 确定按钮颜色
        .okIsBold(true)

        .negativeText(android.R.string.cancel) // 取消
        .cancelSize(12)
        .negativeColorRes(R.color.gray) // 取消按钮颜色
        .cancelIsBold(false)
        // 设置底部按钮（确定、取消）背景图
        // .btnSelector(R.drawable.ic_settings_black, DialogAction.POSITIVE)

        // 设置底部按钮（确定、取消）竖排
        // .btnStackedGravity(GravityEnum.END)
        // .stackingBehavior(StackingBehavior.ALWAYS)

        .gravity(Gravity.BOTTOM) // 设置Dialog弹出位置
        .widgetColorRes(R.color.app_red) // 设置Dialog样式颜色
        .backgroundColorRes(R.color.white) // 设置Dialog整个背景色
        .canceledOnTouchOutside(false) // 取消外部点击消失dialog


        // 监听某一个底部按钮（确定 or 取消）
        .onAny((dialog, which) -> {
            if (which == DialogAction.POSITIVE)
                Logger.e("ClickListener DialogAction.POSITIVE");
        })

        // 监听底部确定按钮，执行顺序优先于onAny()
        .onPositive((dialog, which) -> {
            Logger.e("onPositive");
            // 清理多选框所有选中
            // dialog.clearSelectedIndices();
            // dialog.dismiss();
        })

        // 监听Dialog展示
        .showListener(dialogInterface -> Logger.e("Dialog Show Listener"))

        // 监听Dialog点击取消
        .cancelListener(dialogInterface -> Logger.e("Dialog Cancel Listener"))

        // 监听Dialog消失
        .dismissListener(dialogInterface -> Logger.e("Dialog Dismiss Listener"))

        // 单选框（不想监听，最后listener填写null）
        .checkBoxSize(12)
        .checkBoxColor(R.color.orange_red)
        .checkBoxPrompt("同意", true, (buttonView, isChecked) -> {
            if (isChecked) Logger.e("CheckBox Selected");
        })

        // 设置内容，如果是简单的列表数据
//                .items(arrays)
//                .itemsCallback((dialog, itemView, which, text) -> {
//                    Logger.e("ItemClick position -> " + which + " / text -> " + text);
//                })
//                // 当Item点击、Item长按共存时，这个属性必须添加（否则长按后dialog.dismiss）
//                .autoDismiss(false)
//                // 设置列表数据长按操作，例如删除
//                .itemsLongCallback((dialog, itemView, position, text) -> {
//                    Logger.e("LongPress position -> " + position + " / text -> " + text);
//                    if (dialog.getItems() != null) dialog.getItems().remove(position);
//                    dialog.notifyItemsChanged();
//
//                    // 往列表中添加一条数据（显示在末尾）
//                    // dialog.getItems().add("Add Item" + (position + 1));
//                    // dialog.notifyItemInserted(dialog.getItems().size() - 1);
//                    return false;
//                })

        // 设置单选框
//                .itemsDisabledIndices(1, 3) // 取消焦点，不允许选择
//                // 不想默认选择，第一个参数：-1
//                .itemsCallbackSingleChoice(2, (dialog, itemView, which, text) -> {
//                    Logger.e("SingleChoice position -> " + which + " / text -> " + text);
//                    return true;
//                })

        // 设置多选框
//                .itemsCallbackMultiChoice(
//                        // 不想默认选择，第一个参数：Integer[]{}
//                        new Integer[]{1, 3}, (dialog, which, text) -> {
//                            StringBuilder str = new StringBuilder();
//                            for (int i = 0; i < which.length; i++) {
//                                if (i > 0) {
//                                    str.append('\n');
//                                }
//                                str.append(which[i]);
//                                str.append(": ");
//                                str.append(text[i]);
//                            }
//                            Logger.e("MultiChoice onSelection -> \n" + str.toString());
//                            return true;

        // 需要配合使用：.alwaysCallMultiChoiceCallback()
//                            boolean allowSelectionChange = which.length <= 2;
//                            if (!allowSelectionChange) {
//                                Logger.e("必须小于等于2个选择");
//                            }
//                            return allowSelectionChange;

//                            // 需要配合使用：.alwaysCallMultiChoiceCallback()
//                            boolean allowSelectionChange = which.length >= 1;
//                            if (!allowSelectionChange) {
//                                Logger.e("必须大于等于1个选择");
//                            }
//                            return allowSelectionChange;

//                        })
//                // 一直监听多选框，勾选就调用回调。
//                 .alwaysCallMultiChoiceCallback()
//                // 确定、取消无法dialog.dismiss
//                // .autoDismiss(false)
//                // 设置灰色无法操作
//                .itemsDisabledIndices(1, 3)

        // 设置输入框
        .inputTextSize(18)
        .inputTextColor(R.color.black)
        .inputHintColor(R.color.orange_light)
        .inputType( // 输入类型
                InputType.TYPE_CLASS_TEXT
                        | InputType.TYPE_TEXT_VARIATION_PERSON_NAME
                        | InputType.TYPE_TEXT_FLAG_CAP_WORDS)
        .inputRange(2, 16) // 输入区间，字数2~16
        // 第一个参数hint，第二个参数填充的text
        .input(
                "111",
                "222",
                false,
                (dialog, input) -> {
                    Logger.e("Hello, " + input.toString() + "!");
//                            if (input.length() < 2 || input.length() > 16) {
//                                dialog.getActionButton(DialogAction.POSITIVE).setEnabled(false);
//                            } else {
//                                dialog.getActionButton(DialogAction.POSITIVE).setEnabled(true);
//                            }
                })
//                .alwaysCallInputCallback()

        .show();

### 自定义CommonDialog说明：
dialog = new CommonDialog.Builder(this, R.layout.dialog_show)
        .customIcon(R.drawable.ic_okay_green)
        .customClose(R.drawable.ic_close_black)
        .customOkResId(android.R.string.ok)
        .customCancelResId(android.R.string.cancel)
        .customTitleResId(R.string.app_name)
        .customContent("大号字体内容")
        .customSubContent("小号字体内容")
        .cancelable(false)
        .onPositive((dialog, which) -> {
            Logger.e("onPositive");
            this.dialog.dismiss();
        })
        .onNegative((dialog, which) -> {
            Logger.e("onNegative");
            this.dialog.dismiss();
        })
        .show();

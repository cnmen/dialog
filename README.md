### If you don't know, please click here : [CmonBaby](https://www.cmonbaby.com)

## Material Dialog ![Build Status](https://travis-ci.org/greenrobot/EventBus.svg?branch=master)

## About Material Dialog Code (2016-12-15)

### DialogHelper All API：
```java
new DialogHelper.Builder(this)
        .title(R.string.app_name)
        .titleGravity(GravityEnum.START)
        .titleSize(25)
        .titleColorRes(R.color.orange_dark)

        .iconRes(R.mipmap.ic_launcher)
        .limitIconToDefaultSize()

        .content("")
        .contentGravity(GravityEnum.START)
        .contentSize(12)
        .contentColorRes(R.color.green_dark)

        .positiveText(android.R.string.ok)
        .okSize(15)
        .positiveColorRes(R.color.black)
        .okIsBold(true)

        .negativeText(android.R.string.cancel)
        .cancelSize(12)
        .negativeColorRes(R.color.gray)
        .cancelIsBold(false)
        // .btnSelector(R.drawable.ic_settings_black, DialogAction.POSITIVE)

        // .btnStackedGravity(GravityEnum.END)
        // .stackingBehavior(StackingBehavior.ALWAYS)

        .gravity(Gravity.BOTTOM)
        .widgetColorRes(R.color.app_red)
        .backgroundColorRes(R.color.white)
        .canceledOnTouchOutside(false)


        .onAny((dialog, which) -> {
            if (which == DialogAction.POSITIVE)
                Logger.e("ClickListener DialogAction.POSITIVE");
        })

        .onPositive((dialog, which) -> {
            Logger.e("onPositive");
            // dialog.clearSelectedIndices();
            // dialog.dismiss();
        })

        .showListener(dialogInterface -> Logger.e("Dialog Show Listener"))

        .cancelListener(dialogInterface -> Logger.e("Dialog Cancel Listener"))

        .dismissListener(dialogInterface -> Logger.e("Dialog Dismiss Listener"))

        .checkBoxSize(12)
        .checkBoxColor(R.color.orange_red)
        .checkBoxPrompt("agree", true, (buttonView, isChecked) -> {
            if (isChecked) Logger.e("CheckBox Selected");
        })

//                .items(arrays)
//                .itemsCallback((dialog, itemView, which, text) -> {
//                    Logger.e("ItemClick position -> " + which + " / text -> " + text);
//                })
//                .autoDismiss(false)
//                .itemsLongCallback((dialog, itemView, position, text) -> {
//                    Logger.e("LongPress position -> " + position + " / text -> " + text);
//                    if (dialog.getItems() != null) dialog.getItems().remove(position);
//                    dialog.notifyItemsChanged();
//
//                    // dialog.getItems().add("Add Item" + (position + 1));
//                    // dialog.notifyItemInserted(dialog.getItems().size() - 1);
//                    return false;
//                })

//                .itemsDisabledIndices(1, 3)
//                .itemsCallbackSingleChoice(2, (dialog, itemView, which, text) -> {
//                    Logger.e("SingleChoice position -> " + which + " / text -> " + text);
//                    return true;
//                })

//                .itemsCallbackMultiChoice(
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

//                            boolean allowSelectionChange = which.length <= 2;
//                            if (!allowSelectionChange) {
//                                Logger.e("<=2");
//                            }
//                            return allowSelectionChange;

//                            boolean allowSelectionChange = which.length >= 1;
//                            if (!allowSelectionChange) {
//                                Logger.e(">=1");
//                            }
//                            return allowSelectionChange;

//                        })
//                 .alwaysCallMultiChoiceCallback()
//                // .autoDismiss(false)
//                .itemsDisabledIndices(1, 3)

        .inputTextSize(18)
        .inputTextColor(R.color.black)
        .inputHintColor(R.color.orange_light)
        .inputType(
                InputType.TYPE_CLASS_TEXT
                        | InputType.TYPE_TEXT_VARIATION_PERSON_NAME
                        | InputType.TYPE_TEXT_FLAG_CAP_WORDS)
        .inputRange(2, 16)
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
```

### CustomView Dialog Coding：
```java
dialog = new CommonDialog.Builder(this, R.layout.dialog_show)
        .customIcon(R.drawable.ic_okay_green)
        .customClose(R.drawable.ic_close_black)
        .customOkResId(android.R.string.ok)
        .customCancelResId(android.R.string.cancel)
        .customTitleResId(R.string.app_name)
        .customContent("")
        .customSubContent("")
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
```


Via Gradle:
```gradle
implementation 'com.cmonbaby:material_dialog:1.0.0'
```

Via Maven:
```xml
<dependency>
    <groupId>com.cmonbaby</groupId>
    <artifactId>material_dialog</artifactId>
    <version>1.0.0</version>
</dependency>
```

## License

Copyright (C) 2013-2020 Markus Junginger, Simon (https://www.cmonbaby.com)
Material Dialog binaries and source code can be used according to the [Apache License, Version 2.0](LICENSE).
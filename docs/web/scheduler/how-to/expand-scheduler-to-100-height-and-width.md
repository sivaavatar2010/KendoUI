---
title: Expand Scheduler to 100% Width and Height
page_title: Expand Scheduler to 100% Width and Height | Kendo UI Scheduler Widget
description: "Learn how to expand a Kendo UI Scheduler widget to a width and height of 100%."
slug: howto_expand_scheduler_to100percent_widthandheight_scheduler
---

# Expand Scheduler to 100% Width and Height

Kendo UI Scheduler automatically expands horizontally, and you do not need to explicitly set a 100% width style.

As for the height of the Scheduler, note the following:

* Elements with a percentage height require you to explicitly set a height to their parent. This rule applies recursively until either an element with a pixel height, or the `<html>` element is reached.
* 100% high elements cannot have borders, paddings, margins, or visible siblings.
* When the page content expands to the full browser window height and uses its own internal scrollbar, the default page scrollbar should be removed.

The example below demonstrates how to expand the Scheduler to 100% height and width. 

###### Example

```html

<style>
html
{
    font: 12px sans-serif;
    overflow: hidden;
}

html,
body,
#example,
#scheduler
{
    margin: 0;
    padding: 0;
    height: 100%;
    border-width: 0;
}
</style>

<div id="example" class="k-content">
    <div id="scheduler"></div>
</div>
  
<script>
$(function() {
    $("#scheduler").kendoScheduler({
        date: new Date("2013/6/13"),
        startTime: new Date("2013/6/13 07:00 AM"),
        views: [
            "day",
            { type: "week", selected: true },
            "month",
            "agenda",
            "timeline"
        ],
        timezone: "Etc/UTC",
        dataSource: {
            batch: true,
            transport: {
                read: {
                    url: "http://demos.telerik.com/kendo-ui/service/meetings",
                    dataType: "jsonp"
                },
                update: {
                    url: "http://demos.telerik.com/kendo-ui/service/meetings/update",
                    dataType: "jsonp"
                },
                create: {
                    url: "http://demos.telerik.com/kendo-ui/service/meetings/create",
                    dataType: "jsonp"
                },
                destroy: {
                    url: "http://demos.telerik.com/kendo-ui/service/meetings/destroy",
                    dataType: "jsonp"
                },
                parameterMap: function(options, operation) {
                    if (operation !== "read" && options.models) {
                        return {models: kendo.stringify(options.models)};
                    }
                }
            },
            schema: {
                model: {
                    id: "meetingID",
                    fields: {
                        meetingID: { from: "MeetingID", type: "number" },
                        title: { from: "Title", defaultValue: "No title", validation: { required: true } },
                        start: { type: "date", from: "Start" },
                        end: { type: "date", from: "End" },
                        startTimezone: { from: "StartTimezone" },
                        endTimezone: { from: "EndTimezone" },
                        description: { from: "Description" },
                        recurrenceId: { from: "RecurrenceID" },
                        recurrenceRule: { from: "RecurrenceRule" },
                        recurrenceException: { from: "RecurrenceException" },
                        roomId: { from: "RoomID", nullable: true },
                        attendees: { from: "Attendees", nullable: true },
                        isAllDay: { type: "boolean", from: "IsAllDay" }
                    }
                }
            }
        },
        resources: [
            {
                field: "roomId",
                dataSource: [
                    { text: "Meeting Room 101", value: 1, color: "#6eb3fa" },
                    { text: "Meeting Room 201", value: 2, color: "#f58a8a" }
                ],
                title: "Room"
            },
            {
                field: "attendees",
                dataSource: [
                    { text: "Alex", value: 1, color: "#f8a398" },
                    { text: "Bob", value: 2, color: "#51a0ed" },
                    { text: "Charlie", value: 3, color: "#56ca85" }
                ],
                multiple: true,
                title: "Attendees"
            }
        ]
    });
});
</script>

```

## See Also 

Other articles and how-to examples on Kendo UI Scheduler:

* [JavaScript API Reference](/api/javascript/ui/scheduler)
* [How to Add Controls to Custom Editor]({% slug howto_add_controlsto_custom_event_editor_scheduler %})
* [How to Add Events Programatically]({% slug howto_add_events_programatically_scheduler %})
* [How to Calculate Scheduler Height Dynamically]({% slug howto_calculate_scheduler_height_dunamically_scheduler %})
* [How to Calculate Scheduler Height Dynamically on Mobile]({% slug howto_calculate_scheduler_height_dunamically_onmobile_scheduler %})
* [How to Clone Events on `Ctrl`+`move`]({% slug howto_clone_eventson_ctrlplus_move_scheduler %})
* [How to Create Custom Views Inheriting Built-In Views]({% slug howto_create_custom_view_inheriting_builtinview_scheduler %})
* [How to Create Custom `month` View with Event Count in **Show More** Button]({% slug howto_create_custom_monthview_eventcount_showmore_button_scheduler %})
* [How to Create Custom Restrictions]({% slug howto_create_custom_restrivtions_scheduler %})
* [How to Customize Edit and Events Templates]({% slug howto_customize_editand_event_templates_scheduler %})
* [How to Create External Editor Form]({% slug howto_create_external_editor_form_scheduler %})
* [How to Edit Records on `touchend`]({% slug howto_edit_records_using_touchendonmobile_scheduler %})
* [How to Edit Using ContextMenu]({% slug howto_edit_using_kendouicontextmenu_scheduler %})
* [How to Filter Events by Resource Using MultiSelect]({% slug howto_filter_eventsby_resourceusing_multiselect_scheduler %})
* [How to Get `next` Occurance]({% slug howto_getthe_next_occurance_scheduler %})
* [How to Get Reference to the Built-In Validator]({% slug howto_get_referencetothe_builtin_validator_scheduler %})
* [How to Hide Edit Buttons]({% slug howto_hidethe_editbutons_scheduler %})
* [How to Implement Custom Editing in `agenda` View]({% slug howto_implement_custom_editing_inagenda_view_scheduler %})
* [How to Nest Editors inside Event Templates]({% slug howto_nest_editorsinside_event_templates_scheduler %})
* [How to Use Custom Event Template with Specific Background Color]({% slug howto_use_custom_event_templatewith_specific_background_color_scheduler %})

How-to examples on Kendo UI Scheduler in AngularJS:

* [How to Create and Set `ObservableArray` Events]({% slug howto_createand_set_observablearray_events_angularjs_scheduler %})
* [How to Edit Using ContextMenu]({% slug howto_edit_using_contectmenu_angularjs_scheduler %})
* [How to Set Initial Data Manually]({% slug howto_set_intial_data_manually_angularjs_scheduler %})
* [How to Show Тooltip on `hover`]({% slug howto_show_tooltipon_hover_angularjs_scheduler %})
* [How to Wrap Scheduler in Custom Directives]({% slug howto_wrap_schedulerin_custom_directives_angularjs_scheduler %})

For additional runnable examples on Kendo UI Scheduler, browse the [Scheduler **How To** documentation folder](http://docs.telerik.com/kendo-ui/web/scheduler/how-to).
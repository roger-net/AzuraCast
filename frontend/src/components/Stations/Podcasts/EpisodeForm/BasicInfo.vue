<template>
    <tab
        :label="$gettext('Basic Information')"
        :item-header-class="tabClass"
    >
        <div class="row g-3">
            <form-group-field
                id="form_edit_title"
                class="col-md-6"
                :field="v$.title"
                :label="$gettext('Episode')"
            />

            <form-group-field
                id="form_edit_link"
                class="col-md-6"
                :field="v$.link"
                :label="$gettext('Website')"
                :description="$gettext('Typically a website with content about the episode.')"
            />

            <form-group-field
                id="form_edit_description"
                class="col-md-12"
                :field="v$.description"
                input-type="textarea"
                :label="$gettext('Description')"
                :description="$gettext('The description of the episode. The typical maximum amount of text allowed for this is 4000 characters.')"
            />

            <form-group-field
                id="form_edit_publish_date"
                class="col-md-6"
                input-type="date"
                :field="v$.publish_date"
                :label="$gettext('Publish Date')"
                :description="$gettext('The date when the episode should be published.')"
            />

            <form-group-field
                id="form_edit_publish_time"
                class="col-md-6"
                input-type="time"
                :field="v$.publish_time"
                :label="$gettext('Publish Time')"
                :description="$gettext('The time when the episode should be published (according to the stations timezone).')"
            />

            <form-group-checkbox
                id="form_edit_explicit"
                class="col-md-12"
                :field="v$.explicit"
                :label="$gettext('Contains explicit content')"
                :description="$gettext('Indicates the presence of explicit content (explicit language or adult content). Apple Podcasts displays an Explicit parental advisory graphic for your episode if turned on. Episodes containing explicit material aren\'t available in some Apple Podcasts territories.')"
            />

            <form-group-field
                id="form_edit_season_number"
                class="col-md-6"
                :field="v$.season_number"
                input-type="number"
                :input-attrs="{ step: '1' }"
                :label="$gettext('Season Number')"
                :description="$gettext('Optionally list this episode as part of a season in some podcast aggregators.')"
                clearable
            />

            <form-group-field
                id="form_edit_episode_number"
                class="col-md-6"
                :field="v$.episode_number"
                input-type="number"
                :input-attrs="{ step: '1' }"
                :label="$gettext('Episode Number')"
                :description="$gettext('Optionally set a specific episode number in some podcast aggregators.')"
                clearable
            />
        </div>
    </tab>
</template>

<script setup lang="ts">
import FormGroupField from "~/components/Form/FormGroupField.vue";
import FormGroupCheckbox from "~/components/Form/FormGroupCheckbox.vue";
import {useVModel} from "@vueuse/core";
import {useVuelidateOnFormTab} from "~/functions/useVuelidateOnFormTab";
import {required} from "@vuelidate/validators";
import Tab from "~/components/Common/Tab.vue";

const props = defineProps({
    form: {
        type: Object,
        required: true
    }
});

const emit = defineEmits(['update:form']);
const form = useVModel(props, 'form', emit);

const {v$, tabClass} = useVuelidateOnFormTab(
    {
        title: {required},
        link: {},
        description: {required},
        publish_date: {},
        publish_time: {},
        explicit: {},
        season_number: {},
        episode_number: {}
    },
    form,
    {
        title: '',
        link: '',
        description: '',
        publish_date: '',
        publish_time: '',
        explicit: false,
        season_number: null,
        episode_number: null
    }
);
</script>

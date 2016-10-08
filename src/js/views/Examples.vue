<template>
    <div>
        <h2 id="debounce-example" class="content-subhead"><a href="#debounce-example">Delayed Validation (Debounced)</a></h2>
        <p>
            You can specify a delay to debounce the input event, a case scenario that you may want to wait for the user to stop typing then validate the field.
            This can be achieved by adding a <code class="inline">data-delay</code> attribute on the field being validated, and assign it the number of milliseconds you want to wait for.
        </p>
        <delay-example></delay-example>
        <h2 id="reject-example" class="content-subhead"><a href="#reject-example">Reject Invalid Files</a></h2>
        <p>
            After validating a file, you may want to reject the uploaded file if it fails the validation, this can be done by adding
            the <code class="inline">reject</code> modifier to directive. so you would use it like this: <code class="inline">v-validate.reject</code>.
            <div class="note">
                <b>Note: </b> The <code>reject</code> modifier is only relevant on file inputs, adding it to other input types will not have an effect.
            </div>
        </p>
        <reject-example></reject-example>
        <h2 id="validate-data-example" class="content-subhead"><a href="#validate-data-example">Validate $data</a></h2>
        <p>
            The basic approach relies on listening to the <code class="inline">input</code> or the <code class="inline">change</code> events depending on the file type.
            However most of the time, your values are bound to your Vue instance and some code may change their inputs programatically, the basic approach won't detect this change.
            <br><br>
            <b class="important">The Solution:</b> The <code class="inline">v-validate</code> directive can take a binding expression, the expression is the data name you wish to validate. for example:
            <code-block class="language-html">
                &lt;input v-validate=&quot;email&quot; data-rules=&quot;required|email&quot; type=&quot;text&quot; name=&quot;email&quot;&gt;
            </code-block>
            Whenever the binding value is updated, the validator will validate the new value automatically.
            <div class="note">
                <b>Note:</b> The plugin will use the data in your vue instance as the source of the input value, meaning it won't be watching the input anymore.
                And as you noticed, you don't need to provide a <code>name</code> attribute, as the expression name will be used instead.
            </div>
         </p>
         <data-example></data-example>
         <p>
            <div class="note">
                <b>Note:</b> Notice that the <code>email</code> field was immediatly validated when you open the page, you may not want this behavior, use the <code>initial</code> modifier to tell the validator to ignore the first evaluation like this: <code>v-validate.initial</code>.
                <br>For example the name field above didn't display any errors when you opened this page.
                This attribute is only relevant when validating using binding expressions, it has no effect otherwise.
            </div>
            <br>
            <div class="note">
                <b>Note:</b> When you provide a binding expression to the directive, <code>delay</code> attribute and <code>reject</code> modifier won't have an effect anymore. so you might want to handle debouncing the inputs yourself.
            </div>
         </p>
         <h2 id="validate-form" class="content-subhead"><a href="#validate-form">Validate Form Before Submit</a></h2>
         <p>
            You may want to trigger all inputs validation before submitting a form, maybe display an alert or prevent form submission if any errors are detected.
         </p>
         <event-example></event-example>
         <h2 id="locale-example" class="content-subhead"><a href="#locale-example">Localized Messages</a></h2>
         <p>
            You may want to display error messages in different languages, here is an example on how you may do that. The language below is Arabic (RTL):
         </p>
         <locale-example></locale-example>
         <p>
            <div class="note">
                <b>Note: </b> Here we are also seeing <code>data-as</code> attribute which tells the validator to use that value as the field name when generating error messages, this is a good way to display 'pretty names' for your inputs in error messages, which would make sense when displaying messages in other languages.
                <br><br>Keep in mind that those pretty names are only used when generating error messages.
            </div>
         </p>
         <h2 id="scope-example" class="content-subhead"><a href="#scope-example">Scopes</a></h2>
         <p>
            By default the scope of the validator is the same as the Vue instance that owns it, sometimes you may have multiple fields with the same name, they are in different forms and serve different purposes.
            The validator will then treat those two fields as the same field which will cause problems detecting the input and displaying the errors.
            <br><br>
            You can tell the validator to scope the fields by adding a <code class="inline">data-scope</code> attribute which tells the validator the name of the scope. Those fields will be then identified using their name and their scope. allowing duplicate fields to exist within the same component.
            <br><br>
            For convienece you may add the <code class="inline">data-scope</code> on the form that owns the inputs, you don't have to add the attribute on each and every input.
         </p>
         <scope-example></scope-example>
         <h2 id="coupon-example" class="content-subhead"><a href="#coupon-example">Custom Rule: Coupon</a></h2>
         <p>
            Let's say you want to validate something specific to your app domain that isn't provided by the default validators,
            for example lets validate a user coupon on checkout. If it is a valid coupon then you discount it for him, if not he pays the full price :(
            <br>

            Here is a list of our valid coupons: <code class="inline">SUMMER2016</code>, <code class="inline">WINTER2016</code> and <code class="inline">FALL2016</code>. each of which gives 20% off.

            The process of validation is as follows: we take the input and send it to backend, the response should determine if the coupon is valid which is up to you. here I'm simulating async behavior using <code class="inline">setTimeout</code>.

            <code class="inline">Vee-Validate</code> allows the usage of async validators, but it requires them to return a promise that resolves with an object containing the property <code class="inline">valid</code> which should equal a boolean state of the validation status.
         </p>
         <coupon-example></coupon-example>
         <h2 id="radio-buttons-example" class="content-subhead"><a href="#radio-buttons-example">Radio Buttons</a></h2>
         <p>
            vee-validate also supports validating radio buttons, you can use whatever rules you want on them but only few rules makes sense, like <code class="inline">required</code>.
            One thing to note in this example is that you only need to use the directive on one of the radio buttons, you don't need to attach it on every one, they all have to share the same name though.
            <br><br>
            In the following example, the third value is not included using the rule <code class="inline">in:1,2</code>
         </p>
         <radio-buttons-example></radio-buttons-example>
    </div>
</template>

<script>
import DelayExample from './../components/examples/DelayExample.vue';
import LocaleExample from './../components/examples/LocaleExample.vue';
import RejectExample from './../components/examples/RejectExample.vue';
import ScopeExample from './../components/examples/ScopeExample.vue';
import DataExample from './../components/examples/DataExample.vue';
import EventExample from './../components/examples/EventExample.vue';
import CouponExample from './../components/examples/CouponExample.vue';
import RadioButtonsExample from './../components/examples/RadioButtonsExample.vue';

export default {
    components: {
        DelayExample,
        LocaleExample,
        RejectExample,
        ScopeExample,
        DataExample,
        EventExample,
        CouponExample,
        RadioButtonsExample
    }
};
</script>
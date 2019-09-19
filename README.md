# A LIST OF FORM VALIDATION RULES FOR LARAVEL
A quick reference I run and check when working on complex form validations rules with laravel. Tips are from the official laravel documentation

**accepted**

The field under validation must be yes, on, 1, or true. This is useful for validating "Terms of Service" acceptance.

active_url

The field under validation must have a valid A or AAAA record according to the dns_get_record PHP function.

after:date

The field under validation must be a value after a given date. The dates will be passed into the strtotime PHP function:

'start_date' => 'required|date|after:tomorrow'

Instead of passing a date string to be evaluated by strtotime, you may specify another field to compare against the date:

'finish_date' => 'required|date|after:start_date'

after_or_equal:date

The field under validation must be a value after or equal to the given date. For more information, see the after rule.

alpha

The field under validation must be entirely alphabetic characters.

alpha_dash

The field under validation may have alpha-numeric characters, as well as dashes and underscores.

alpha_num

The field under validation must be entirely alpha-numeric characters.

array

The field under validation must be a PHP array.

bail

Stop running validation rules after the first validation failure.

before:date

The field under validation must be a value preceding the given date. The dates will be passed into the PHP strtotime function. In addition, like the after rule, the name of another field under validation may be supplied as the value of date.

before_or_equal:date

The field under validation must be a value preceding or equal to the given date. The dates will be passed into the PHP strtotime function. In addition, like the after rule, the name of another field under validation may be supplied as the value of date.

between:min,max

The field under validation must have a size between the given min and max. Strings, numerics, arrays, and files are evaluated in the same fashion as the size rule.

boolean

The field under validation must be able to be cast as a boolean. Accepted input are true, false, 1, 0, "1", and "0".

confirmed

The field under validation must have a matching field of foo_confirmation. For example, if the field under validation is password, a matching password_confirmation field must be present in the input.

date

The field under validation must be a valid, non-relative date according to the strtotime PHP function.

date_equals:date

The field under validation must be equal to the given date. The dates will be passed into the PHP strtotime function.

date_format:format

The field under validation must match the given format. You should use either date or date_format when validating a field, not both. This validation rule supports all formats supported by PHP's DateTime class.

different:field

The field under validation must have a different value than field.

digits:value

The field under validation must be numeric and must have an exact length of value.

digits_between:min,max

The field under validation must have a length between the given min and max.

dimensions

The file under validation must be an image meeting the dimension constraints as specified by the rule's parameters:

'avatar' => 'dimensions:min_width=100,min_height=200'

Available constraints are: min_width, max_width, min_height, max_height, width, height, ratio.

A ratio constraint should be represented as width divided by height. This can be specified either by a statement like 3/2 or a float like 1.5:

'avatar' => 'dimensions:ratio=3/2'

Since this rule requires several arguments, you may use the Rule::dimensions method to fluently construct the rule:

use Illuminate\Validation\Rule;

Validator::make($data, [
    'avatar' => [
        'required',
        Rule::dimensions()->maxWidth(1000)->maxHeight(500)->ratio(3 / 2),
    ],
]);

distinct

When working with arrays, the field under validation must not have any duplicate values.

'foo.*.id' => 'distinct'

email

The field under validation must be formatted as an e-mail address. Under the hood, this validation rule makes use of the egulias/email-validator package for validating the email address. By default the RFCValidation validator is applied, but you can apply other validation styles as well:

'email' => 'email:rfc,dns'

The example above will apply the RFCValidation and DNSCheckValidation validations. Here's a full list of validation styles you can apply:

    rfc: RFCValidation
    strict: NoRFCWarningsValidation
    dns: DNSCheckValidation
    spoof: SpoofCheckValidation
    filter: FilterEmailValidation

The filter validator, which uses PHP's filter_var function under the hood, ships with Laravel and is Laravel's pre-5.8 behavior.

ends_with:foo,bar,...

The field under validation must end with one of the given values.

exists:table,column

The field under validation must exist on a given database table.
Basic Usage Of Exists Rule

'state' => 'exists:states'

If the column option is not specified, the field name will be used.
Specifying A Custom Column Name

'state' => 'exists:states,abbreviation'

Occasionally, you may need to specify a specific database connection to be used for the exists query. You can accomplish this by prepending the connection name to the table name using "dot" syntax:

'email' => 'exists:connection.staff,email'

If you would like to customize the query executed by the validation rule, you may use the Rule class to fluently define the rule. In this example, we'll also specify the validation rules as an array instead of using the | character to delimit them:

use Illuminate\Validation\Rule;

Validator::make($data, [
    'email' => [
        'required',
        Rule::exists('staff')->where(function ($query) {
            $query->where('account_id', 1);
        }),
    ],
]);

file

The field under validation must be a successfully uploaded file.

filled

The field under validation must not be empty when it is present.

gt:field

The field under validation must be greater than the given field. The two fields must be of the same type. Strings, numerics, arrays, and files are evaluated using the same conventions as the size rule.

gte:field

The field under validation must be greater than or equal to the given field. The two fields must be of the same type. Strings, numerics, arrays, and files are evaluated using the same conventions as the size rule.

image

The file under validation must be an image (jpeg, png, bmp, gif, svg, or webp)

in:foo,bar,...

The field under validation must be included in the given list of values. Since this rule often requires you to implode an array, the Rule::in method may be used to fluently construct the rule:

use Illuminate\Validation\Rule;

Validator::make($data, [
    'zones' => [
        'required',
        Rule::in(['first-zone', 'second-zone']),
    ],
]);

in_array:anotherfield.*

The field under validation must exist in anotherfield's values.

integer

The field under validation must be an integer.

    This validation rule does not verify that the input is of the "integer" variable type, only that the input is a string or numeric value that contains an integer.

ip

The field under validation must be an IP address.
ipv4

The field under validation must be an IPv4 address.
ipv6

The field under validation must be an IPv6 address.

json

The field under validation must be a valid JSON string.

lt:field

The field under validation must be less than the given field. The two fields must be of the same type. Strings, numerics, arrays, and files are evaluated using the same conventions as the size rule.

lte:field

The field under validation must be less than or equal to the given field. The two fields must be of the same type. Strings, numerics, arrays, and files are evaluated using the same conventions as the size rule.

max:value

The field under validation must be less than or equal to a maximum value. Strings, numerics, arrays, and files are evaluated in the same fashion as the size rule.

mimetypes:text/plain,...

The file under validation must match one of the given MIME types:

'video' => 'mimetypes:video/avi,video/mpeg,video/quicktime'

To determine the MIME type of the uploaded file, the file's contents will be read and the framework will attempt to guess the MIME type, which may be different from the client provided MIME type.

mimes:foo,bar,...

The file under validation must have a MIME type corresponding to one of the listed extensions.
Basic Usage Of MIME Rule

'photo' => 'mimes:jpeg,bmp,png'

Even though you only need to specify the extensions, this rule actually validates against the MIME type of the file by reading the file's contents and guessing its MIME type.

A full listing of MIME types and their corresponding extensions may be found at the following location: https://svn.apache.org/repos/asf/httpd/httpd/trunk/docs/conf/mime.types

min:value

The field under validation must have a minimum value. Strings, numerics, arrays, and files are evaluated in the same fashion as the size rule.

not_in:foo,bar,...

The field under validation must not be included in the given list of values. The Rule::notIn method may be used to fluently construct the rule:

use Illuminate\Validation\Rule;

Validator::make($data, [
    'toppings' => [
        'required',
        Rule::notIn(['sprinkles', 'cherries']),
    ],
]);

not_regex:pattern

The field under validation must not match the given regular expression.

Internally, this rule uses the PHP preg_match function. The pattern specified should obey the same formatting required by preg_match and thus also include valid delimiters. For example: 'email' => 'not_regex:/^.+$/i'.

Note: When using the regex / not_regex patterns, it may be necessary to specify rules in an array instead of using pipe delimiters, especially if the regular expression contains a pipe character.

nullable

The field under validation may be null. This is particularly useful when validating primitive such as strings and integers that can contain null values.

numeric

The field under validation must be numeric.

present

The field under validation must be present in the input data but can be empty.

regex:pattern

The field under validation must match the given regular expression.

Internally, this rule uses the PHP preg_match function. The pattern specified should obey the same formatting required by preg_match and thus also include valid delimiters. For example: 'email' => 'regex:/^.+@.+$/i'.

Note: When using the regex / not_regex patterns, it may be necessary to specify rules in an array instead of using pipe delimiters, especially if the regular expression contains a pipe character.

required

The field under validation must be present in the input data and not empty. A field is considered "empty" if one of the following conditions are true:

    The value is null.
    The value is an empty string.
    The value is an empty array or empty Countable object.
    The value is an uploaded file with no path.

required_if:anotherfield,value,...

The field under validation must be present and not empty if the anotherfield field is equal to any value.

If you would like to construct a more complex condition for the required_if rule, you may use the Rule::requiredIf method. This methods accepts a boolean or a Closure. When passed a Closure, the Closure should return true or false to indicate if the field under validation is required:

use Illuminate\Validation\Rule;

Validator::make($request->all(), [
    'role_id' => Rule::requiredIf($request->user()->is_admin),
]);

Validator::make($request->all(), [
    'role_id' => Rule::requiredIf(function () use ($request) {
        return $request->user()->is_admin;
    }),
]);

required_unless:anotherfield,value,...

The field under validation must be present and not empty unless the anotherfield field is equal to any value.

required_with:foo,bar,...

The field under validation must be present and not empty only if any of the other specified fields are present.

required_with_all:foo,bar,...

The field under validation must be present and not empty only if all of the other specified fields are present.

required_without:foo,bar,...

The field under validation must be present and not empty only when any of the other specified fields are not present.

required_without_all:foo,bar,...

The field under validation must be present and not empty only when all of the other specified fields are not present.

same:field

The given field must match the field under validation.

size:value

The field under validation must have a size matching the given value. For string data, value corresponds to the number of characters. For numeric data, value corresponds to a given integer value. For an array, size corresponds to the count of the array. For files, size corresponds to the file size in kilobytes.

starts_with:foo,bar,...

The field under validation must start with one of the given values.

string

The field under validation must be a string. If you would like to allow the field to also be null, you should assign the nullable rule to the field.

timezone

The field under validation must be a valid timezone identifier according to the timezone_identifiers_list PHP function.

unique:table,column,except,idColumn

The field under validation must not exist within the given database table.

Specifying A Custom Column Name:

The column option may be used to specify the field's corresponding database column. If the column option is not specified, the field name will be used.

'email' => 'unique:users,email_address'

Custom Database Connection

Occasionally, you may need to set a custom connection for database queries made by the Validator. As seen above, setting unique:users as a validation rule will use the default database connection to query the database. To override this, specify the connection and the table name using "dot" syntax:

'email' => 'unique:connection.users,email_address'

Forcing A Unique Rule To Ignore A Given ID:

Sometimes, you may wish to ignore a given ID during the unique check. For example, consider an "update profile" screen that includes the user's name, e-mail address, and location. You will probably want to verify that the e-mail address is unique. However, if the user only changes the name field and not the e-mail field, you do not want a validation error to be thrown because the user is already the owner of the e-mail address.

To instruct the validator to ignore the user's ID, we'll use the Rule class to fluently define the rule. In this example, we'll also specify the validation rules as an array instead of using the | character to delimit the rules:

use Illuminate\Validation\Rule;

Validator::make($data, [
    'email' => [
        'required',
        Rule::unique('users')->ignore($user->id),
    ],
]);

    You should never pass any user controlled request input into the ignore method. Instead, you should only pass a system generated unique ID such as an auto-incrementing ID or UUID from an Eloquent model instance. Otherwise, your application will be vulnerable to an SQL injection attack.

Instead of passing the model key's value to the ignore method, you may pass the entire model instance. Laravel will automatically extract the key from the model:

Rule::unique('users')->ignore($user)

If your table uses a primary key column name other than id, you may specify the name of the column when calling the ignore method:

Rule::unique('users')->ignore($user->id, 'user_id')

By default, the unique rule will check the uniqueness of the column matching the name of the attribute being validated. However, you may pass a different column name as the second argument to the unique method:

Rule::unique('users', 'email_address')->ignore($user->id),

Adding Additional Where Clauses:

You may also specify additional query constraints by customizing the query using the where method. For example, let's add a constraint that verifies the account_id is 1:

'email' => Rule::unique('users')->where(function ($query) {
    return $query->where('account_id', 1);
})

url

The field under validation must be a valid URL.

uuid

The field under validation must be a valid RFC 4122 (version 1, 3, 4, or 5) universally unique identifier (UUID).




Conditionally Adding Rules
Validating When Present

In some situations, you may wish to run validation checks against a field only if that field is present in the input array. To quickly accomplish this, add the sometimes rule to your rule list:

$v = Validator::make($data, [
    'email' => 'sometimes|required|email',
]);

In the example above, the email field will only be validated if it is present in the $data array.

    If you are attempting to validate a field that should always be present but may be empty, check out this note on optional fields

Complex Conditional Validation

Sometimes you may wish to add validation rules based on more complex conditional logic. For example, you may wish to require a given field only if another field has a greater value than 100. Or, you may need two fields to have a given value only when another field is present. Adding these validation rules doesn't have to be a pain. First, create a Validator instance with your static rules that never change:

$v = Validator::make($data, [
    'email' => 'required|email',
    'games' => 'required|numeric',
]);

Let's assume our web application is for game collectors. If a game collector registers with our application and they own more than 100 games, we want them to explain why they own so many games. For example, perhaps they run a game resale shop, or maybe they just enjoy collecting. To conditionally add this requirement, we can use the sometimes method on the Validator instance.

$v->sometimes('reason', 'required|max:500', function ($input) {
    return $input->games >= 100;
});

The first argument passed to the sometimes method is the name of the field we are conditionally validating. The second argument is the rules we want to add. If the Closure passed as the third argument returns true, the rules will be added. This method makes it a breeze to build complex conditional validations. You may even add conditional validations for several fields at once:

$v->sometimes(['reason', 'cost'], 'required', function ($input) {
    return $input->games >= 100;
});

    The $input parameter passed to your Closure will be an instance of Illuminate\Support\Fluent and may be used to access your input and files.

Validating Arrays

Validating array based form input fields doesn't have to be a pain. You may use "dot notation" to validate attributes within an array. For example, if the incoming HTTP request contains a photos[profile] field, you may validate it like so:

$validator = Validator::make($request->all(), [
    'photos.profile' => 'required|image',
]);

You may also validate each element of an array. For example, to validate that each e-mail in a given array input field is unique, you may do the following:

$validator = Validator::make($request->all(), [
    'person.*.email' => 'email|unique:users',
    'person.*.first_name' => 'required_with:person.*.last_name',
]);

Likewise, you may use the * character when specifying your validation messages in your language files, making it a breeze to use a single validation message for array based fields:

'custom' => [
    'person.*.email' => [
        'unique' => 'Each person must have a unique e-mail address',
    ]
],

Custom Validation Rules

Using Rule Objects

Laravel provides a variety of helpful validation rules; however, you may wish to specify some of your own. One method of registering custom validation rules is using rule objects. To generate a new rule object, you may use the make:rule Artisan command. Let's use this command to generate a rule that verifies a string is uppercase. Laravel will place the new rule in the app/Rules directory:

php artisan make:rule Uppercase

Once the rule has been created, we are ready to define its behavior. A rule object contains two methods: passes and message. The passes method receives the attribute value and name, and should return true or false depending on whether the attribute value is valid or not. The message method should return the validation error message that should be used when validation fails:

<?php

namespace App\Rules;

use Illuminate\Contracts\Validation\Rule;

class Uppercase implements Rule
{
    /**
     * Determine if the validation rule passes.
     *
     * @param  string  $attribute
     * @param  mixed  $value
     * @return bool
     */
    public function passes($attribute, $value)
    {
        return strtoupper($value) === $value;
    }

    /**
     * Get the validation error message.
     *
     * @return string
     */
    public function message()
    {
        return 'The :attribute must be uppercase.';
    }
}

You may call the trans helper from your message method if you would like to return an error message from your translation files:

/**
 * Get the validation error message.
 *
 * @return string
 */
public function message()
{
    return trans('validation.uppercase');
}

Once the rule has been defined, you may attach it to a validator by passing an instance of the rule object with your other validation rules:

use App\Rules\Uppercase;

$request->validate([
    'name' => ['required', 'string', new Uppercase],
]);

Using Closures

If you only need the functionality of a custom rule once throughout your application, you may use a Closure instead of a rule object. The Closure receives the attribute's name, the attribute's value, and a $fail callback that should be called if validation fails:

$validator = Validator::make($request->all(), [
    'title' => [
        'required',
        'max:255',
        function ($attribute, $value, $fail) {
            if ($value === 'foo') {
                $fail($attribute.' is invalid.');
            }
        },
    ],
]);

Using Extensions

Another method of registering custom validation rules is using the extend method on the Validator facade. Let's use this method within a service provider to register a custom validation rule:

<?php

namespace App\Providers;

use Illuminate\Support\ServiceProvider;
use Illuminate\Support\Facades\Validator;

class AppServiceProvider extends ServiceProvider
{
    /**
     * Register any application services.
     *
     * @return void
     */
    public function register()
    {
        //
    }

    /**
     * Bootstrap any application services.
     *
     * @return void
     */
    public function boot()
    {
        Validator::extend('foo', function ($attribute, $value, $parameters, $validator) {
            return $value == 'foo';
        });
    }
}

The custom validator Closure receives four arguments: the name of the $attribute being validated, the $value of the attribute, an array of $parameters passed to the rule, and the Validator instance.

You may also pass a class and method to the extend method instead of a Closure:

Validator::extend('foo', 'FooValidator@validate');

Defining The Error Message

You will also need to define an error message for your custom rule. You can do so either using an inline custom message array or by adding an entry in the validation language file. This message should be placed in the first level of the array, not within the custom array, which is only for attribute-specific error messages:

"foo" => "Your input was invalid!",

"accepted" => "The :attribute must be accepted.",

// The rest of the validation error messages...

When creating a custom validation rule, you may sometimes need to define custom placeholder replacements for error messages. You may do so by creating a custom Validator as described above then making a call to the replacer method on the Validator facade. You may do this within the boot method of a service provider:

/**
 * Bootstrap any application services.
 *
 * @return void
 */
public function boot()
{
    Validator::extend(...);

    Validator::replacer('foo', function ($message, $attribute, $rule, $parameters) {
        return str_replace(...);
    });
}

Implicit Extensions

By default, when an attribute being validated is not present or contains an empty string, normal validation rules, including custom extensions, are not run. For example, the unique rule will not be run against an empty string:

$rules = ['name' => 'unique:users,name'];

$input = ['name' => ''];

Validator::make($input, $rules)->passes(); // true

For a rule to run even when an attribute is empty, the rule must imply that the attribute is required. To create such an "implicit" extension, use the Validator::extendImplicit() method:

Validator::extendImplicit('foo', function ($attribute, $value, $parameters, $validator) {
    return $value == 'foo';
});

    An "implicit" extension only implies that the attribute is required. Whether it actually invalidates a missing or empty attribute is up to you.

Implicit Rule Objects

If you would like a rule object to run when an attribute is empty, you should implement the Illuminate\Contracts\Validation\ImplicitRule interface. This interface serves as a "marker interface" for the validator; therefore, it does not contain any methods you need to implement.
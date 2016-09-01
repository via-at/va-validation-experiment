# va-validation-experiment
A web component which supports data validation

**This repository has been deprecated. Use [via-at/va-validation](https://github.com/via-at/va-validation) instead.**

## Installation

```
bower install via-at/va-validation-experiment
```

## Usage

va-validation-behavior makes an element validator. This element should locate in form element and bind data between input elements. All data is validated when it is updated.
If errors are occured, each error message can be visible and notify invalid field is true. Also, if the validator has any one of errors, valid property is false. It is useful to enable or disable button element.

Here is an example of validator. It validates user profiles containing `firstName`, `lastName` and `phoneNumber`.
The `firstName` and `lastName` are required, but `phoneNumber` is optional. If `phoneNumber` is set, validates with `isPhoneNumber` method.
```
<dom-module id="my-user-validator">

  <script>
    Polymer({
      is: 'my-user-validator',
      properties: {
        fields: {
          value: {
            firstName: {
              required: true
            },
            lastName: {
              required: true
            },
            phoneNumber: {
              empty: true,
              rules: ['isPhoneNumber']
            }
          }
        },
        
        messages: {
          value: {
            // The key must be validation rule name.
            firstName: {
              required: 'Your first name is required.'
            },
            lastName: {
              required: 'Your last name is required.'
            },
            phoneNumber: {
              isPhoneNumber: 'Your phone number is invald format.'
            }
          }
        }
      },
      
      isPhoneNumber: function (phoneNumber) {
        return /* validates the value is phone number. */;
      }
    });
  </script>
  
</dom-module>
```

After defining a validator, you can add it to the form element as a child.
```
<form>
  <my-user-validator
    data="[[data]]"
    validation="{{validation}}"
    error-messages="{{errorMessages}}"
    valid="{{valid}}"></my-user-validator>
    
  <paper-input
    value="{{data.firstName}}"
    error-message="{{errorMessages.firstName}}"
    invalid="{{!validation.firstName}}"></paper-input>

  <paper-input
    value="{{data.lastName}}"
    error-message="{{errorMessages.lastName}}"
    invalid="{{!validation.lastName}}"></paper-input>
    
  <paper-input
    value="{{data.phoneNumber}}"
    error-message="{{errorMessages.phoneNumber}}"
    invalid="{{!validation.phoneNumber}}"></paper-input>
    
  <paper-button disabled="[[!valid]]">Submit!</paper-button>
</form>
```

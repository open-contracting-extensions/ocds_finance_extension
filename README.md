# Financing extension

Sometimes, particularly in the case of Public Private Partnerships, contracts are financed using a range of instruments, including loans, grants, share issues and so-on.

The financing extension provides a space to declare the finance arranged for a contract.

This is declared within the `contracts` section, based on an understanding that this information is generally only disclosed following the signature of a contract. This information can be updated over the lifetime of the contract.

The finance building block includes:

* **Title** and **Description** - for providing summary information about the finance
* **Financing Party** - an organization reference to the id and name of an organization listed in the main parties array.
* **Finance Type** - an entry from a FinanceType codelist
* **Finance Category** - an entry from a Finance Category codelist
* **Step in arrangements** and **Exchange rate guarantee** flags, to indicate whether either apply to this finance
* **Repayment Frequency** - to give an indication of likely repayments
* **Period** - a start, end date and/or duration for the finance
* **interestRate** - an object consisting of:
  * **base** - a constant such as 0.1, or a known rate such as LIBOR
  * **margin** - the component added to this base to give the rate
  * **fixed** - a boolean for whether the rate is fixed or variable
  * **notes** - space to provide more information on the rate

This allows modelling of rates such as 'LIBOR+1%'.

## Codelists

The 'financeType' codelist is based on the list on [Page 57 of the World Bank PPP Disclosure Framework](http://pubdocs.worldbank.org/en/143671469558797229/FrameworkPPPDisclosure-071416.pdf#page=57)

The 'financeCategory' codelist is used to indicate (a) the rights attached to finance (in terms of equity, mezzanine and senior loans), and (b) to distinguish direct finance from guarantees.

## Example

```json
{
  "contracts": [
    {
      "id": "1",
      "awardID": "1",
      "title": "Public Private Partnership Agreement",
      "description": "Public-Private Partnership agreement entered into by and between telecoms promoter, together with national fibre infrastructure and the special purpose vehicle Mega Consortium Ltd",
      "finance": [
        {
          "id": "1",
          "title": "Primary senior debt financing agreement",
          "description": "Big Bank Corp retains the right to step in should Mega Consortium fail to comply with the repayment schedule for a period of 3 consecutive months.",
          "financingParty": {
            "id": "XX-FI-22222222",
            "name": "Big Bank Corp"
          },
          "financeCategory": "seniorDebt",
          "value": {
            "amount": 41000000,
            "currency": "USD"
          },
          "period": {
            "startDate": "2016-01-24T00:00:00Z",
            "endDate": "2021-01-23T00:00:00Z"
          },
          "interestRate": {
            "base": "LIBOR",
            "margin": 0.03,
            "fixed": false
          },
          "stepInRights": true,
          "exchangeRateGuarantee": false,
          "repaymentFrequency": 30.4
        },
        {
          "id": "2",
          "title": "Alpha Holdings equity investment",
          "financingParty": {
            "id": "XX-XXX-11111111",
            "name": "Alpha Holdings Ltd"
          },
          "financeCategory": "equity",
          "value": {
            "amount": 6674000,
            "currency": "USD"
          }
        }
      ]
    }
  ]
}
```

## Issues

Report issues for this extension in the [ocds-extensions repository](https://github.com/open-contracting/ocds-extensions/issues), putting the extension's name in the issue's title.

## Changelog

### 2019-03-20

* Set `"uniqueItems": true` on array fields, and add `"minLength": 1` on required string fields.
* Make `interestRate` non-nullable (undo earlier change).

### 2018-05-08

* Make `Finance.id` required and non-nullable to support revision tracking and [list merging](http://standard.open-contracting.org/latest/en/schema/merging/#lists)

### 2018-05-01

* Add title and description to `Finance.financingParty`.

### 2018-01-29

* Make `interestRate` nullable.

# Examples of API requests.

Here are the example API queries. Please notice that they are only to work in graphql interface. For use by curl, etc, they should be placed in the query string.

_**createOrganization - creates organization.**_

```graphql
  mutation createOrganization {
    createOrganization(input: {
      name: "OrganizationName",
      about: "Organization description text",
      analyticId: "analyticId"
    }) {
      organization {
        node {
          id
          name
          about
          analyticId
        }
      }
    }
  }
```

_**createOrganizationProfile - creates organizationProfile.**_

```
mutation createOrganizationProfile {
    createOrganizationProfile(input: {}) {
      organizationProfile {
        node {
          id
        }
      }
    }
  }
```

_**addOrganizationHasManyOrganizationProfiles - connects organization and organizationProfile.**_

```
mutation addOrganizationHasManyOrganizationProfiles {
    addOrganizationHasManyOrganizationProfiles(input: {
      organization: "id_organization_from_createOrganization_payload",
      organizationProfile: "id_organization_from_createOrganizationProfile_payload",
    }) {
      organization {
        id
        organizationProfiles {
          edges {
            node {
              id
            }
          }
        }
      }
    }
  }
```

_**getOrganization - returns organization by id**_

```
  query getOrganization {
    organization(id: "id_organization_from_createOrganization_payload") {
      name
      about
      analyticId
      organizationProfiles {
        edges {
          node {
            id
          }
        }
      }
    }
  }
```

_**getOrganizations - returns the first 200 Organization, with other data**_

```
query getOrganizations {
    organizations(first: 200) {
      edges {
        node {
          id
          name
          about
          status {
            id
            key
            value
          }
          analyticId
          media {
            url
            type {
              id
              value
              key
            }
          }
          contacts {
            edges {
              node {
                id
                address {
                  street
                  zip
                  postalCode
                  country {
                    id
                    value
                    key
                  }
                  city {
                    id
                    value
                    key
                  }
                }
                phone {
                  id
                  value
                  type
                }
                webContact {
                  id
                  value
                  type
                }
              }
            }
          }
          organizationProfiles {
            edges {
              node {
                id
                profileType{
                  id
                  key
                  value
                }
                userOrganizationProfiles {
                  edges {
                    node {
                      user {
                        id
                        fullName
                        firstName
                        lastName
                        userName
                        media {
                          id
                          url
                          type {
                            id
                            key
                            value
                          }
                        }
                      }
                    }
                  }
                }
              }
            }
          }
          socialAccounts {
            edges {
              node {
                id
                url
                title
                type
                login
              }
            }
          }
          banking {
            achisomoch {
              id
              locationName
            }
            stripe {
              id
              locationName
              accountNumber
              verification
              displayOnStatement
              country {
                id
                key
                value
              }
              currency {
                id
                key
                value
              }
            }
            creditCard {
              id
              status
              locationName
              usernameApi
              passwordApi
              urlApi
              midApi
              urlDash
            }
            ach {
              id
              status
              banking
              currency {
                id
                key
                value
              }
            }
            paypal {
              id
            }
          }
        }
      }

    }
  }
```

_**updateOrganization - updates organization by id**_

```
mutation updateOrganization {
    updateOrganization(input: {
      id: "id_organization_from_createOrganization_payload",
      name: "NewName",
      analyticId: "newanalyticId",
      about: "New Description"
    }) {
      organization {
        id
        name
        analyticId
      }
    }
  }
```

_**removeOrganizationHasManyOrganizationProfiles - unset the connection between the organization and organizationProfile**_

```
mutation removeOrganizationHasManyOrganizationProfiles {
    removeOrganizationHasManyOrganizationProfiles(input: {
      organization: "id_organization_from_createOrganization_payload",
      organizationProfile: "id_organization_from_createOrganizationProfile_payload",
    }) {
      organization {
        id
        organizationProfiles {
          edges {
            node {
              id
            }
          }
        }
      }
    }
  }
```

_**removeOrganization - delete organization by id**_

```
mutation removeOrganization {
    removeOrganization(input: {
      id: "id_organization_from_createOrganization_payload"
    }) {
      organization {
        id
        name
        analyticId
      }
    }
  }
```




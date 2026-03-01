# GitHub Projects v2 GraphQL snippets

## Find a project by owner + number

```graphql
query ($login: String!, $number: Int!) {
  user(login: $login) {
    projectV2(number: $number) {
      ...ProjectV2Details
    }
  }
  organization(login: $login) {
    projectV2(number: $number) {
      ...ProjectV2Details
    }
  }
}

fragment ProjectV2Details on ProjectV2 {
  id
  title
  url
  number
  fields(first: 50) {
    nodes {
      ... on ProjectV2Field {
        id
        name
        dataType
      }
      ... on ProjectV2SingleSelectField {
        id
        name
        dataType
        options {
          id
          name
        }
      }
      ... on ProjectV2IterationField {
        id
        name
        dataType
        configuration {
          iterations {
            id
            title
            startDate
            duration
          }
        }
      }
    }
  }
}
```

## Add issue/PR to project

```graphql
mutation ($projectId: ID!, $contentId: ID!) {
  addProjectV2ItemById(
    input: { projectId: $projectId, contentId: $contentId }
  ) {
    item {
      id
    }
  }
}
```

## Update field values

### Single select

```graphql
mutation ($projectId: ID!, $itemId: ID!, $fieldId: ID!, $optionId: String!) {
  updateProjectV2ItemFieldValue(
    input: {
      projectId: $projectId
      itemId: $itemId
      fieldId: $fieldId
      value: { singleSelectOptionId: $optionId }
    }
  ) {
    projectV2Item {
      id
    }
  }
}
```

### Date

```graphql
mutation ($projectId: ID!, $itemId: ID!, $fieldId: ID!, $date: Date!) {
  updateProjectV2ItemFieldValue(
    input: {
      projectId: $projectId
      itemId: $itemId
      fieldId: $fieldId
      value: { date: $date }
    }
  ) {
    projectV2Item {
      id
    }
  }
}
```

### Iteration

```graphql
mutation ($projectId: ID!, $itemId: ID!, $fieldId: ID!, $iterationId: String!) {
  updateProjectV2ItemFieldValue(
    input: {
      projectId: $projectId
      itemId: $itemId
      fieldId: $fieldId
      value: { iterationId: $iterationId }
    }
  ) {
    projectV2Item {
      id
    }
  }
}
```

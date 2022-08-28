# 174. Rendering Card Groups

**index.js** - Rendering Card Groups
```
import React, { Component } from "react";
import { Card } from "semantic-ui-react";
import factory from "../ethereum/factory";

class CampaignIndex extends Component {
  static async getInitialProps() {
    const campaigns = await factory.methods.getDeployedCampaigns().call();

    return { campaigns };
  }
  renderCampaigns() {
    const items = this.props.campaigns.map((address) => {
      return {
        header: address,
        description: <a>View Campaign</a>,
        fluid: true,
      };
    });
    return <Card.Group items={items} />;
  }
  render() {
    return <div>{this.renderCampaigns()}</div>;
  }
}

export default CampaignIndex;
```

<details>
  <summary>Render - result capture</summary>

![174.1_Rendering-Card-Groups.png](../imgs/174.1_Rendering-Card-Groups.png)
---
</details>

##  Resources for this lecture

---

-   [178-rendering-card.zip](https://beatlesm.s3.us-west-1.amazonaws.com/ethereum-and-solidity-complete-developer-guide/178-rendering-card.zip)
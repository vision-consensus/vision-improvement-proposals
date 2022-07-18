# VIPs

Vision Improvement Proposals (VIPs) describe standards for the Vision platform, including core protocol specifications, client APIs, and contract standards.

****

## Contents
 * [VIPs](#vips)
    * [VIPs Guide](#vips-guide)
    * [To Submit a VIP](#to-submit-a-tip)
    * [VIP Status](#vip-status)
    * [VIP Types](#vip-types)
****

## VIPs Guide 


| ID     | Title                                            |        Author        | Type | Category | Hard&nbsp;fork | Status |
|--------|--------------------------------------------------|:--------------------:| :----: |:--------:|:--------------:| :----: |
| VIP 01 | SpreadMint                                       | darylc9527@gmail.com | Standards Track  |   Core   |      true      | Final |
| VIP 02     | Ethereum Transaction Compatible                  | darylc9527@gmail.com | Standards Track  |   Core   |     false      | Final |
| VIP 03     | Vision Economy Model                             | darylc9527@gmail.com | Standards Track  |   Core   |      false      | Final |
| VIP 04     | Sort Witness not by block                        | darylc9527@gmail.com | Standards Track  |   Core   |      false      | Final |
| VIP 05     | JSON RPC                                         | darylc9527@gmail.com | Standards Track  |   API    |      false      | Final |
| VIP 06     | Adjust the total photon limit                    | darylc9527@gmail.com | Standards Track  |   API    |      false      | Final |
| VIP 07     | Adjust the pledge period or clear vote           | darylc9527@gmail.com | Standards Track  |   CORE   |      false      | Final |
| VIP 08     | Adjust the pledge rate and optimize JsonRpc apis | darylc9527@gmail.com | Standards Track  |   API    |      false      | Final |
| VIP 09     | JsonRpc API optimize                             | darylc9527@gmail.com | Standards Track  |   API    |      false      | Final |
| VIP 20     | VRC-20 Token Standard                            | darylc9527@gmail.com | Standards Track  |   VRC    |      false      | Final |
| VIP 721    | VRC-721 Non-Fungible Token Standard              | darylc9527@gmail.com | Standards Track  |   VRC    |      false      | Final |
| ----   | ----                                             |        :----:        | :----: |  :----:  |     :----:     | :----: |
****

## To Submit a VIP

Before you submit a VIP, you need to create an issue for comment and add the issue URL to your VIP header.   

1.&nbsp;Fork the repository by clicking "Fork" in the top right.  

2.&nbsp;Add your VIP to your fork of the repository. There is a [VIP template](https://github.com/vision-consensus/VIPs/blob/master/template.md) here.  

3.&nbsp;Submit a Pull Request to Vision's VIPs repository.

Your first PR should be a first draft of the final VIP. It must meet the formatting criteria enforced by the build (largely, correct metadata in the header). An editor will manually review the first PR for a new VIP and assign it a number before merging it. 

Make sure you include a discussions-to header with the URL to a discussion forum or open GitHub issue where people can discuss the VIP as a whole. If a VIP is about the feature development of vision-core, and a PR of the development exists, in your VIP and your vision-core's PR you need to refer each other's github link.

When you believe your VIP is mature and ready to progress past the draft phase, you should do one of two things:

- For a Standards Track VIP of type Core, ask to have your issue added to the agenda of an upcoming All Core Devs meeting, where it can be discussed for inclusion in a future hard fork. If implementers agree to include it, the VIP editors will update the state of your VIP to 'Accepted'. 

- For all other VIPs, open a PR changing the state of your VIP to 'Final'. An editor will review your draft and ask if anyone objects to its being finalized. If the editor decides there is no rough consensus, they may close the PR and request you fix the issues in the draft before trying again.

****

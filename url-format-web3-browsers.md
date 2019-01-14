---
eip: <to be assigned>
title: URL Format for Web3 Browsers
author: Bruno Barbieri (@brunobar79)
discussions-to: <URL>
status: Draft
type: Standards Track
category: ERC
created: 01/13/2019
requires: 831
---

<!--You can leave these HTML comments in your merged EIP and delete the visible duplicate text guides, they will not appear and may be helpful to refer to if you edit it again. This is the suggested template for new EIPs. Note that an EIP number will be assigned by an editor. When opening a pull request to submit your EIP, please use an abbreviated title in the filename, `eip-draft_title_abbrev.md`. The title should be 44 characters or less.-->
This is the suggested template for new EIPs.

## Simple Summary
A standard way of representing web3 browser URLs for decentralized applications.

## Abstract
<!--A short (~200 word) description of the technical issue being addressed.-->
Since most normal web browsers (specifically on mobile devices) can not run decentralized applications correctly because of the lack of web3 support, it is necessary to differentiate them from normal urls, so they can be opened in 
web3 browsers if available.

## Motivation
<!--The motivation is critical for EIPs that want to change the Ethereum protocol. It should clearly explain why the existing protocol specification is inadequate to address the problem that the EIP solves. EIP submissions without sufficient motivation may be rejected outright.-->
Lots of dApps that are trying to improve their mobile experience are currently (deep)linking to specific mobile web3 browsers which are using their own url scheme. 
In order to make the experience more seamless, dApps should still be able to recommend a specific mobile web3 browser via [deferred deeplinking](https://en.wikipedia.org/wiki/Deferred_deep_linking) but by having a standard url format, if the user already has a web3 browser installed that implements this standard, it will be automatically linked to it.

## Specification
<!--The technical specification should describe the syntax and semantics of any new feature. The specification should be detailed enough to allow competing, interoperable implementations for any of the current Ethereum platforms (go-ethereum, parity, cpp-ethereum, ethereumj, ethereumjs, and [others](https://github.com/ethereum/wiki/wiki/Clients)).-->

### Syntax

Web3 browser URLs contain "ethereum" in their schema (protocol) part and are constructed as follows:


    request                 = erc831_part - http_prefix "/" dapp_url [ "?" parameters [ chain_id_parameter ] ]
    erc831_part             = schema and optional prefix as defined in #831 - typically "ethereum" ":" [ "dapp-" ] in this case
    http_prefix             = "http" / "https"
    parameters              = parameter *( "&" parameter )
    parameter               = key "=" value
    chain_id_parameter      = chain_id "=" chain_id_value
    chain_id_value          = 1*DIGIT
    key                     = STRING
    number                  = [ "-" / "+" ] *DIGIT [ "." 1*DIGIT ] [ ( "e" / "E" ) [ 1*DIGIT ] [ "+" UNIT ]
 
 ### Semantics

`chain_id_parameter` is optional and it is a parameter for the browser to select the corresponding chain and it will not be passed to the dApp.

This a complete example url:

`ethereum:dapp-https/peepeth.com/brunobar79?chain_id=1&utm_source=twitter`;

which will open the web3 browser, select 'mainnet' (chain_id = 1) and then navigate to `https://peepeth.com/brunobar79?&utm_source=twitter`

## Rationale
<!--The rationale fleshes out the specification by describing what motivated the design and why particular design decisions were made. It should describe alternate designs that were considered and related work, e.g. how the feature is supported in other languages. The rationale may also provide evidence of consensus within the community, and should discuss important objections or concerns raised during discussion.-->
The proposed format attempts to solve the problem of vendor specific protocols for the web3  while additional features like the `chain_id_parameter` which will help avoid using dApps in the wrong network.

## References

1. ERC-831, https://eips.ethereum.org/EIPS/eip-831

## Copyright
Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).

# metadata
contract-metadata
A mapping of checksummed Ethereum contract addresses to metadata, like names, and images of their logos.

All address keys follow the EIP 55 address checksum format. All file keys follow the CAIP 19 asset id format.

This repository is effectively frozen. We recommend that developers of new tokens use EIP 747 to ask the user's permission to display your tokens in their wallet. This reduces the dangers of airdrop-based phishing, and reduces administrative overhead from managing this list.

Usage
You can install from npm with npm install @metamask/contract-metadata and use it in your code like this:

import contractMap from '@metamask/contract-metadata'
import ethJSUtil from 'ethereumjs-util'
const { toChecksumAddress } = ethJSUtil

function imageElForEVMToken (chainId, address) {
  const caip19Address = `eip155:${chainId}/erc20:${toChecksumAddress(address)}`
  const metadata = contractMap[caip19Address]
  if (metadata?.logo) {
    const fileName = metadata.logo
    const path = `${__dirname}/${metadata.logo}`
    const img = document.createElement('img')
    img.src = path
    img.style.width = '100%'
    return img
  }
}
// to get ethereum erc20 token img el
const ethereumNetworkChainId = 1
imageElForEVMToken (ethereumNetworkChainId,"")

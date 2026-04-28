# Soulbound-Badge-System
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

contract SoulboundBadge {
    mapping(address => mapping(uint256 => bool)) public hasBadge;
    uint256 public badgeCount;

    event BadgeIssued(address indexed to, uint256 badgeId);

    function issueBadge(address to, uint256 badgeId) public {
        require(!hasBadge[to][badgeId], "Badge already issued");
        hasBadge[to][badgeId] = true;
        if (badgeId > badgeCount) badgeCount = badgeId;
        emit BadgeIssued(to, badgeId);
    }

    function hasAnyBadge(address user) public view returns (bool) {
        for (uint256 i = 1; i <= badgeCount; i++) {
            if (hasBadge[user][i]) return true;
        }
        return false;
    }
}

pragma solidity ^0.8.0;

contract MetaArena {
    address public owner;

    struct Player {
        string username;
        uint256 score;
    }

    mapping(address => Player) public players;

    event PlayerRegistered(address indexed player, string username);
    event ScoreUpdated(address indexed player, uint256 newScore);

    modifier onlyOwner() {
        require(msg.sender == owner, "Only owner can perform this action.");
        _;
    }

    constructor() {
        owner = msg.sender;
    }

    function registerPlayer(string calldata _username) external {
        require(bytes(players[msg.sender].username).length == 0, "Player already registered.");

        players[msg.sender] = Player({
            username: _username,
            score: 0
        });

        emit PlayerRegistered(msg.sender, _username);
    }

    function updateScore(address _player, uint256 _score) external onlyOwner {
        require(bytes(players[_player].username).length > 0, "Player not registered.");

        players[_player].score = _score;
        emit ScoreUpdated(_player, _score);
    }

    function getPlayer(address _player) external view returns (string memory username, uint256 score) {
        Player memory p = players[_player];
        return (p.username, p.score);
    }
}

contract MyToken {
    string public name;
    string public symbol;
    uint256 public totalSupply;

    mapping(address => uint256) public balances;

    constructor(string memory _name, string memory _symbol, uint256 _initialSupply) {
        name = _name;
        symbol = _symbol;
        totalSupply = _initialSupply;
        balances[msg.sender] = _initialSupply;
    }

    function mint(address _receiver, uint256 _amount) public {
        require(_amount > 0, "Amount must be greater than 0");
        
        balances[_receiver] += _amount;
        totalSupply += _amount;
    }

    function burn(address _account, uint256 _amount) public {
        require(_amount > 0, "Amount must be greater than 0");
        require(balances[_account] >= _amount, "Insufficient balance");
        
        balances[_account] -= _amount;
        totalSupply -= _amount;
    }
}


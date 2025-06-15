// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;


contract Token value is Ownable {
    address public owner;
    mapping address (mapping => uint256) public balances;
    event DepositedEther(address indexed user, uint256 amount);
    event WithDrawEther(address indexed user, uint256 amount);
    modifier(onlyOwner == owner, "you are not the owner");
    _;
    consturctor(){
        msg.sender = owner;

    }
    //To deposit Ether into the contract
    function DepositEther() external only owner{
        require(msg.value > 0, "The amount of ether must be greater than zero" );
        balances[msg.sender] += msg.value;
        emit Etherdeposit(msg.sender, msg.value);

    //The function to withdraw the ether from the vault
    function WithdrawEther(uint256 amount) external only owner{
        require(balances(msg.sender)>=amount, "insufficent Ether");
        balances[msg.sender]-=amount;
        payable(msg.sender).transfer(amount);
        emit Withdrawn(uint256 amount, msg.sender);

        //the owner can pause the valut for security purposes
        function pauseVault() external only owner{
            paused = true;
            emit paused();
            
            
        }
        //the owner can also unpause the vault
        function UmpauseVault() external only owner{
            paused = false;
            emit umpaused();

       }
       //To prevent accidental Ether transactions 
       receive() external payable{
           revert("Use Deposit()");
       }

        

    }

        
    }

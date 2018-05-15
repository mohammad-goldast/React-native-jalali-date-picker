# React-native-jalali-date-picker
A simple and clean jalali datepicker for ReactNative.

My goal of push this package on github is to use it for personal projects. You can refer to the below link and use the full version of this package : [https://github.com/rghorbani/react-native-general-calendars]: React-Native-General-calendars

## Demo
<kbd>
  <img src="https://raw.githubusercontent.com/blackhair/React-native-jalali-datepicker/master/demo/demo.jpg?raw=true">
</kbd>


## How to use 
Run : 
    
    $ npm i --save react-native-jalali-date-picker
    
Add the following code to the `App.js` of the project :

`A custom prototype for Persian Number`

    Object.defineProperty(String.prototype, 'PersianNumber', {
        value() {
            const num = this.toString();
            let i = 0;        
            const len = num.length;
            let res = '';
            for (; i < len; i++) {
                if (numbers[num.charAt(i)]) {
                    res += numbers[num.charAt(i)];
                } else {
                    res += num.charAt(i);
                }
            }
            return res;
        },
        enumerable: false
    });
    
Add the following code in your component :

    import PersianCalendarPicker from 'React-native-jalali-datepicker';
        class FreeTime extends Component { 
            constructor(props) {
                super(props);

                this.state = {
                    date: new Date(),
                    prevDay: (d => new Date(d.setDate(d.getDate() - 1)))(new Date()),
                    prevDays: (d => new Date(d.setDate(d.getDate() - 1)).toJSON().split('T')[0].replace(/-/g, ''))(new Date()),
                };
                this.onDateChange = this.onDateChange.bind(this);
            }
        
            onDateChange(date) {
            this.setState({ date });
            }
            
            render() {
                const { date, prevDay, prevDays } = this.state;
                return (
                    <View style={styles.container}>
                        <PersianCalendarPicker
                            selectedDate={date}
                            onDateChange={this.onDateChange}
                            screenWidth={Dimensions.get('window').width}
                            minDate={prevDay}
                            prevDays={prevDays}
                        />
                    <Text style={styles.selectedDate}> Date: { this.state.date.toString() } </Text>
                </View>
                );
            }
        }

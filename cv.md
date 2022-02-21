# rsschool-cv

## Egor Klenin

### Junior TypeScript/JavaScript Backend Developer

### Contact Information

E-mail: e.g2gor@gmail.com

Linkedin: https://www.linkedin.com/in/e-g1gor/


### Code example

```JavaScript
/** 
 * Human readable duration format
 * https://www.codewars.com/kata/52742f58faf5485cae000b9a
**/

const MINUTE = 60;
const HOUR = MINUTE * 60;
const DAY = HOUR * 24;
const YEAR = DAY * 365;

class TimeFormatter {
  _seconds;

  constructor(seconds) {
    this._seconds = seconds;
  }

  getYears() {
    const years = Math.floor(this._seconds / YEAR);
    return { years, rest: this._seconds % YEAR };
  }

  get years() {
    return this.getYears().years;
  }

  getDays() {
    const { rest } = this.getYears(this._seconds);
    const days = Math.floor(rest / DAY);
    return { days, rest: rest % DAY };
  }

  get days() {
    return this.getDays().days;
  }

  getHours() {
    const { rest } = this.getDays(this._seconds);
    const hours = Math.floor(rest / HOUR);
    return { hours, rest: rest % HOUR };
  }

  get hours() {
    return this.getHours().hours;
  }

  getMinutes() {
    const { rest } = this.getHours(this._seconds);
    const minutes = Math.floor(rest / MINUTE);
    return { minutes, rest: rest % MINUTE };
  }

  get minutes() {
    return this.getMinutes().minutes;
  }

  getSeconds() {
    const { rest } = this.getMinutes(this._seconds);
    return rest;
  }

  get seconds() {
    return this.getSeconds();
  }

  get intervalInfo() {
    return {
      years: this.years,
      days: this.days,
      hours: this.hours,
      minutes: this.minutes,
      seconds: this.seconds,
    };
  }

  /**
   *
   * @param amount
   */
  getPluralEnding(amount) {
    return amount > 1 ? "s" : "";
  }

  /**
   * @param {string[]} messages
   * @param {number} amount
   * @param {string} msg
   */
  addMessage(messages, amount, msg) {
    if (amount) {
      messages.push(`${amount} ${msg}${this.getPluralEnding(amount)}`);
    }
  }

  get humanReadable() {
    if (this._seconds === 0) return "now";
    const { years, days, hours, minutes, seconds } = this.intervalInfo;
    let messages = [];
    this.addMessage(messages, years, "year");
    this.addMessage(messages, days, "day");
    this.addMessage(messages, hours, "hour");
    this.addMessage(messages, minutes, "minute");
    this.addMessage(messages, seconds, "second");

    let result;

    if (messages.length > 1) {
      const lastPiece = messages.pop();
      result = messages.join(", ") + " and " + lastPiece;
    } else {
      result = messages[0];
    }

    return result;
  }
}

/**
 *
 * @param {number} seconds
 */
function formatDuration(seconds) {
  const formatter = new TimeFormatter(seconds);
  return formatter.humanReadable;
}

```

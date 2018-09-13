var request = require('request');
var properties = require('properties-reader')('./properties');

var baseUrl = 'https://pro-api.coinmarketcap.com/v1/';
var headers = {
  'X-CMC_PRO_API_KEY': properties.get('CMC.key')
};
module.exports.getGlobalCapData = function(callback) {
    var args = {
        uri: baseUrl + 'global-metrics/quotes/latest',
        json: true,
        headers: headers
    };
    request.get(args, function(err, data, response) {
        if (err) {
            console.log(err);
            return callback(err);
        }
        return callback(null, response.data);
    });
};
